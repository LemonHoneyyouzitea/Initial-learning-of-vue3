<template>
    <ContentBase>
        <div class="row">
          <div class="col-3">
            <UserProfileInfo @follow="follow" @unfollow="unfollow" :user="user"></UserProfileInfo>
            <UserProfileWrite @post_a_post="post_a_post"></UserProfileWrite>
          </div>
          <div class="col-9">
            <UserProfilePost :posts="posts"></UserProfilePost>
          </div>
        </div>
    </ContentBase>

</template>
  
  <script>
  import ContentBase from '@/components/ContentBase.vue';
  import UserProfileInfo from '@/components/UserProfileInfo.vue'
  import UserProfilePost from '@/components/UserProfilePost.vue'
  import UserProfileWrite from '@/components/UserProfileWrite.vue';
  import { reactive } from 'vue';
  export default {
    name: 'UserProfileView',
    components: {
        ContentBase,
        UserProfileInfo,
        UserProfilePost,
        UserProfileWrite,
    },
    setup() {
      const user = reactive({
        id: 1,
        username: "zhangzhuokun",
        lastName: "Zhang",
        firstName: "Zhuokun",
        followerCount: 0,
        is_followed: false,
      });

      const posts = reactive({
        count: 3,
        posts: [
          {
            id: 1,
            userId: 1,
            content: "今天学了vue真开心"
          },
          {
            id: 2,
            userId: 1,
            content: "今天学了springboot真开心"
          },
          {
            id: 3,
            userId: 1,
            content: "今天学了html真开心"
          },
        ]
      });
      // 函数
      const follow = () => {
        if(user.is_followed) return;
        user.is_followed = true;
        user.followerCount ++ ;
      };
      const unfollow = () => {
        if(!user.is_followed) return;
        user.is_followed =false ;
        user.followerCount -- ;
      };

      const post_a_post = (content) => {
        posts.count ++;
        // push在数组最后加一个元素 , unshift在前面加
        posts.posts.unshift({
          id: posts.count,
          userId: 1,
          content: content
        })
      };
      return {
        user,
        follow,
        unfollow,
        posts,
        post_a_post,
      }
    }
  }
  </script>
  <style scoped>
  
  </style>