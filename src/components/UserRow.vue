<template>
  <tr>
    <td>
      <span v-if="!editable" @click="edit()">{{ user.nickname }}</span>
      <input
        v-show="editable"
        ref="editNickname"
        v-model="user.nickname"
        @blur="user.editable = false"
      />
    </td>
    <td>{{ user.email }}</td>
  </tr>
</template>

<script>
import { defineComponent, ref, nextTick } from '@vue/composition-api';
export function User(nickname, email) {
  this.nickname = nickname;
  this.email = email;
}
export default defineComponent({
  props: {
    user: {
      type: User,
      required: true,
    },
  },
  setup() {
    const editable = ref(false);
    const editNickname = ref(null);
    const edit = () => {
      this.editable = true;
      this.$nextTick(() => {
        //DOM更新後に実行
        this.$refs.editNickname.focus();
      });
    };

    return {
      editable,
      editNickname,
      edit,
    };
  },
});
</script>

<style module>
td input {
  width: 95%;
}
</style>
