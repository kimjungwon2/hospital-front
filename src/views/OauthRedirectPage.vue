<template>
    <div>
    </div>
</template>
 
<script>
export default {
  methods:{
    async oauthLogin(){
      const data ={
        nickName:this.$cookies.get("nick_name"),
        memberId:this.$cookies.get("member_id"),
        memberStatus:this.$cookies.get("member_status"),
        token:this.$cookies.get("token")
      }
      console.log(data);

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
