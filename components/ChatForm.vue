<template>
     <div>
          <v-text-field
            label="Введите сообщение"
            outlined
            v-model="text"
            @keydown.enter="send"
          ></v-text-field>
        </div>
</template>

<script>
export default {
    data: () => ({
        text: ''
    }),
    methods: {
        send() {
            this.$socket.emit('createMessage', {
                text: this.text,
                id: this.$store.state.user.id
            }, data => {
                if(typeof data === 'string') {
                    console.error('ERROR!!!!', data)
                } else {
                    this.text = ''
                }
            })
        }
    }
}
</script>