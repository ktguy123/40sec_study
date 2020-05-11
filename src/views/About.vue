<template>
  <div class="about">
    <div class="overview article">
      <h2>概要</h2>
      <p>学習を終了した後40秒間復習を行うことで、学習定着率が増加します。
      <a href="https://buzz-plus.com/article/2015/11/16/consolidation-of-complex/">参考</a></p>
      <p>そこで、40秒間復習ができるサポートアプリを作成しています。</p>
    </div>

    <div class="use article">
      <h2>つかいかた</h2>
      <p>タイトル欄に入力して、STARTを押下すると開始します。</p>
      <p>40秒間計測されます。学習した内容をできる限り記述してください。</p>
      <p>40秒後に自動終了し、記述した内容が下記に表示されます。</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  h2{
    margin-top:20px;
  }
  .about{
    margin:0 auto;
    max-width:1100px;
    .article{
      border-bottom: 1px black solid;
      p{
        text-align:left;
      }
    }
  }

</style>