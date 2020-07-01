<template>
  <div>
    <div>
      <table>
        <tr>
          <td>思い出Lv</td>
          <td><input /></td>
        </tr>
        <tr>
          <td></td>
          <td>Vo</td>
          <td>Da</td>
          <td>Vi</td>
        </tr>
        <tr>
          <td>現在のステータス</td>
          <td><input /></td>
          <td><input /></td>
          <td><input /></td>
        </tr>
        <tr>
          <td>パッシブバフ</td>
          <td><input /></td>
          <td><input /></td>
          <td><input /></td>
        </tr>
        <tr>
          <td>興味値</td>
          <td><input /></td>
          <td><input /></td>
          <td><input /></td>
        </tr>
        <tr>
          <td>アピール判定</td>
          <td>
            <select>
              <option value="PERFECT">PERFECT</option>
              <option value="GOOD">GOOD</option>
              <option value="NORMAL">NORMAL</option>
              <option value="BAD">BAD</option>
            </select>
          </td>
          <td>何周目？</td>
          <td><input type="number" /></td>
        </tr>
      </table>
    </div>
    // アピール値などを表示します<br />
    <div class="divine">
      <span class="left">
        <div class="judge judge-vo">Vo審査員 100000<br /></div>
        <div class="judge judge-da">Da審査員 50000<br /></div>
        <div class="judge judge-vi">Vi審査員 50000<br /></div>
      </span>
      <span class="right">
        <div class="skill selected">
          <div>
            アルティマ0凸
          </div>
          <div>
            Da4.5倍
          </div>
        </div>
        <div class="skill">
          <div>
            駅まの
          </div>
          <div>
            Da2倍 Vi2倍
          </div>
        </div>
        <div class="skill">
          <div>
            駅まの
          </div>
          <div>
            Da2倍 Vi2倍
          </div>
        </div>
      </span>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped lang="scss">
.divine {
  .left {
    display: inline-block;
    width: 200px;
    .judge {
      display: inline-block;
      height: 50px;
    }
  }
  .right {
    display: inline-block;
    width: 200px;
    .skill {
      &.selected {
        padding-right: 50px;
      }
    }
  }
}
</style>
