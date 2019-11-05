<template>
  <div class="app-container">
    <el-row :gutter="20">
      <el-col :span="6" :xs="24">
        <user-card :user="user" />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import UserCard from '../profile/components/UserCard'
import Activity from '../profile/components/Activity'
import Timeline from '../profile/components/Timeline'
import Account from '../profile/components/Account'

export default {
  name: 'Profile',
  components: { UserCard, Activity, Timeline, Account },
  data() {
    return {
      user: {},
      // activeTab: 'activity'
    }
  },
  computed: {
    ...mapGetters([
      'name',
      'avatar',
      'roles'
    ])
  },
  created() {
    this.getUser()
  },
  methods: {
    getUser() {
      this.user = {
        name: "yingxs",
        role: this.roles.join(' | '),
        email: 'admin@test.com',
        avatar: this.avatar
      }
    }
  }
}

</script>
Expected indentation of 0 spaces but found 2
<style>
</style>
