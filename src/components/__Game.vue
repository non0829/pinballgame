<template>
<div>
  <canvas id="mycanvas" width="500" height="500"></canvas>
</div>
</template>

<script>
export default {
  data() {
    return {
      ball: {
        x: 100,
        y: 200,
        r: 10,
        dx: 10,
        dy: 10,
      },
      bar: {
        x: 100,
        y: 450,
        dx: 10,
      },
      lineLength: 60,
      point: 0,
    };
  },
  methods: {
    drawLine(ctx) {
      ctx.lineCap = "round";
      ctx.lineWidth = 2;
      for (let i = 1; i <= 5; i++) {
        ctx.beginPath();
        ctx.moveTo(100 * i, 0);
        ctx.lineTo(100 * i, this.lineLength);
        ctx.closePath();
        ctx.stroke();
      }
    },
    drawText(ctx) {
      let text = ["10", "-10", "30", "???", "20"];
      ctx.font = "italic bold 20px sans-serif";
      for (let i = 0; i <= 4; i++) {
        if (i === 0) {
          ctx.fillStyle = "#006400";
        } else if (i === 2) {
          ctx.fillStyle = "#FF0461";
        } else if (i === 4) {
          ctx.fillStyle = "#136FFF";
        } else {
          ctx.fillStyle = "black";
        }
        ctx.fillText(text[i], 35 + i * 100, 40, 60);
      }
    },
    drawBall(ctx) {
      ctx.beginPath();
      ctx.fillStyle = "black";
      ctx.arc(
        this.ball.x,
        this.ball.y,
        this.ball.r,
        (Math.PI * 0) / 180,
        (Math.PI * 360) / 180
      );
      ctx.fill();
    },
    drawUnderbar(ctx) {
      ctx.lineWidth = 7;
      ctx.lineCap = "round";

      ctx.beginPath();
      ctx.moveTo(this.bar.x, this.bar.y);
      ctx.lineTo(this.bar.x + 100, this.bar.y);
      ctx.closePath();
      ctx.stroke();
    },
    collide() {
      if (this.ball.y + this.ball.r * 2 === this.bar.y) {
        if (this.ball.x > this.bar.x && this.ball.x < this.bar.x + 100) {
          this.ball.dy *= -1;
        }
        if (this.ball.x > this.bar.x - 20 && this.ball.x <= this.bar.x) {
          this.ball.dy *= -1;
          this.ball.dx *= -1;
        }
        if (this.ball.x > this.bar.x + 100 && this.ball.x <= this.bar.x + 120) {
          this.ball.dy *= -1;
          this.ball.dx *= -1;
        }
      }
    },
    pointCheck() {
      if (this.ball.y - this.ball.r !== 0) {
        return;
      }
      console.log("ポイント追加");
      if (this.ball.x > 0 && this.ball.x < 100) {
        this.$emit("plus10");
      }
      if (this.ball.x > 100 && this.ball.x < 200) {
        this.$emit("minus10");
      }
      if (this.ball.x > 200 && this.ball.x < 300) {
        this.$emit("plus30");
      }
      if (this.ball.x > 300 && this.ball.x < 400) {
        this.ball.dx = Math.floor(Math.random() * 2) + 8;
        this.ball.dy = Math.floor(Math.random() * 2) + 8;
        this.$emit("plusRandom");
      }
      if (this.ball.x > 400 && this.ball.x < 500) {
        this.$emit("plus10");
      }
    },
    reset(ctx) {
      ctx.clearRect(0, 0, 500, 500);
      this.drawLine(ctx);
      this.drawText(ctx);
      this.drawBall(ctx);
      this.drawUnderbar(ctx);
    },
    load(ctx) {
      // 跳ね返す設定
      if (this.ball.x + this.ball.r === 500 || this.ball.x === this.ball.r) {
        this.ball.dx *= -1;
      }
      if (this.ball.y + this.ball.r === 500 || this.ball.y === this.ball.r) {
        this.ball.dy *= -1;
      }
      if (this.ball.y > 0 && this.ball.y < this.lineLength) {
        for (let i = 1; i <= 4; i++) {
          if (this.ball.x + this.ball.r === i * 100) {
            this.ball.dx *= -1;
          }
          if (this.ball.x - this.ball.r === i * 100) {
            this.ball.dx *= -1;
          }
        }
      }

      this.ball.x += this.ball.dx;
      this.ball.y += this.ball.dy;
      this.reset(ctx);

      this.collide();
      this.pointCheck(move);

      // ボールを動かす
      let move = setTimeout(() => {
        this.load(ctx);
      }, 100);

      // 終わり判定
      if (this.ball.y + this.ball.r > 480) {
        console.log("hi");
        clearTimeout(move);
        this.$emit('finish')
      }
    },
  },
  watch: {
    bar: {
      handler: function() {
        let canvas = document.getElementById("mycanvas");
        let ctx = canvas.getContext("2d");
        this.reset(ctx);
      },
      deep: true,
    },
  },
  mounted() {
    let canvas = document.getElementById("mycanvas");
    if (!canvas) return;
    let ctx = canvas.getContext("2d");
    let isStart = false;
    this.reset(ctx);
    // バーを動かす設定
    window.addEventListener("keydown", (e) => {
      if (this.bar.x < 400 && e.key === "ArrowRight") {
        this.bar.x += this.bar.dx;
      }
    });
    window.addEventListener("keydown", (e) => {
      if (this.bar.x > 0 && e.key === "ArrowLeft") {
        this.bar.x -= this.bar.dx;
      }
    });
    // ここまで
    window.addEventListener("keydown", (e) => {
      if (isStart === true) {
        return;
      }
      if (e.key === "Enter") {
        // loadは繰り返し判定
        this.load(ctx);
        isStart = !isStart;
      }
    });
  },
};
</script>

<style scoped>
#mycanvas {
  background-color: rgba(185, 233, 252, 0.377);
}
</style>
