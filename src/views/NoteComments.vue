<template>
    <div>
        <div v-for="comment in note.comments" :key="comment.id">
            <p>{{ comment.commentTitle }}</p>
        </div>
        <!-- title -->
        <!-- input -->
        <!-- comment 1 -->
        <!-- comment 2 -->
        <!-- comment 3 -->
        
    </div>
</template>

<script>


export default {
    name: "note-item",

    data() {
        return {
            
        }
    },
    firestore: {
        
  },
  methods: {
      hey() {
          console.log(this.$route.params.id)
      }
  },
}
</script>