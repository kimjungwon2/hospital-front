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
    async oauthLogin(token){
      this.$cookies.set("token",token, 6 * 30 * 24 * 60 * 60);

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
    const token = this.$route.query.token

    if(token){
      this.oauthLogin(token);
    } else{
      this.$alert('로그인에 실패했습니다.');
      this.$router.push(`/login`);
    }
  }
}
</script>

<style>

</style>
