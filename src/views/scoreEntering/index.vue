<template>
  <div class="app-container">
    <el-row :gutter="20">
     <!-- <el-col :span="6" :xs="24">
        <user-card :user="user" />
      </el-col> -->
      <el-col :span="6" :xs="24">
        <select-and-process-card />
      </el-col>
      <el-col :span="7" :xs="24">
        <student-card :user="user" />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import UserCard from '../profile/components/UserCard'
import StudentCard from './components/StudentCard'
import SelectAndProcessCard from './components/SelectAndProcessCard'

export default {
  name: 'Profile',
  components: { UserCard, StudentCard,SelectAndProcessCard },
  data() {
    return {
      user: {}
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
    console.log(mapGetters)
    this.getUser()
  },
  methods: {
    getUser() {
      this.user = {
        name: 'wujiayao',
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
