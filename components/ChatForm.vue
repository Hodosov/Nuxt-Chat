<template>
     <v-col cols="12" sm="6" md="3">
          <v-text-field
            label="Введите сообщение"
            outlined
            v-model="text"
            @keydown.enter="send"
          ></v-text-field>
        </v-col>
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
                id: this.$store.state.id
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