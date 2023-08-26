<template>
    <div>
    </div>
</template>
 
<script>
import {
    getMemberIdFromCookie, 
    getMemberStatusFromCookie, 
    getNickNameFromCookie, 
    getTokenFromCookie
} from '@/utils/cookies';
 
export default {
  methods:{
    async oauthLogin(){
      const data ={
        nickName:getNickNameFromCookie(),
        memberId:getMemberIdFromCookie(),
        memberStatus:getMemberStatusFromCookie(),
        token:getTokenFromCookie()
      }

      await this.$store.dispatch('oauthLogin',data);
      this.$router.push(`/`);
    }
  },
  created() {
    const loginSuccess = this.$route.query.success

    if(loginSuccess){
      this.oauthLogin();
    } else{
      this.$alert('로그인에 실패했습니다.');
      this.$router.push(`/login`);
    }
  }
}
</script>

<style>

</style>
