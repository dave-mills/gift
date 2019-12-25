<template>
      <div class="hello">
        <h4
        v-for="msg in renderedMsgs"
        :key="msg"
        :class="msg.side"
        class="mb-4"
        >
        {{ msg.msg }}</h4>
        <div style="height: 100px"></div>
        <button class="btn btn-primary"
        v-on:click="nextPos()"
        >Another line...
        </button>

        <form>
            <div class="form-group">
                <label for="incantation">:</label>
                <input type="text" class="form-control" v-model="incantation">
            </div>
        </form>
        <div class="container">
            <img src="../assets/parchment.gif" alt="a large, square, very worn piece of parchment with nothing written on it" class="img-fluid">

            <transition name="fade">
                <img
                    v-if="incantation==required"
                    class="btn img-fluid w-75"
                    src="../assets/ticket-print-transparent.png"
                >
            </transition>
        </div>
        <a
            v-if="incantation==required"
            class="btn btn-lg btn-block btn-success"
            href="../TicketOrder20191222-91590080.pdf"
            @click.prevent="downloadItem(item)"
            >download ticket</a>
    </div>
</template>

<script>

import Axios from 'axios'

    export default {
        name: 'Something',
        data () {
            return {
                msgs: [],
                renderedMsgs: [],
                pos: 0,
                incantation: "",
                required: "I solemnly swear that I am up to no good",
                item: {
                    url: "../TicketOrder20191222-91590080.pdf",
                    label: "Ticket"
                }

            }
        },

        mounted () {
            this.msgs = [
            {
                msg: 'We’ve come to give you a bit of festive cheer before we go. ',
                side: 'text-left',
            },
            {
                msg: 'Come in here…',
                side: 'text-left',

            },
            {
                msg: 'Early Christmas present for you, Emi',
                side: 'text-left',

            },
            {
                msg: 'What’s that supposed to be?',
                side: 'text-right',

            },
            {
                msg: 'This, Emi, is the secret of our success,',
                side: 'text-left',

            },
            {
                msg: 'It’s a wrench, giving it to you, but we decided last night, your need’s greater than ours',
                side: 'text-left',
            },
            {
                msg: 'Anyway, we know it by heart. We bequeath it to you. We don’t really need it anymore',
                side: 'text-left',

            },
            {
                msg: 'And what do I need with a bit of old parchment?',
                side: 'text-right',

            }
            ];

            this.renderedMsgs.push(this.msgs[0]);
        },

        methods: {
            nextPos: function () {

                this.pos++
                this.renderedMsgs.push(this.msgs[this.pos])
            },

            downloadItem ({ url, label }) {
                Axios.get(url, { responseType: 'blob' })
                  .then(({ data }) => {
                    const blob = new Blob([data], { type: 'application/pdf' })
                    const link = document.createElement('a')
                    link.href = URL.createObjectURL(blob)
                    link.download = label
                    link.click()
                  })
                }
        }


    }
</script>

<style>
/* Container needed to position the button. Adjust the width as needed */
.container {
  position: relative;
}

/* Make the image responsive */
.container img {
  width: 100%;
  height: auto;
}

/* Style the button and place it in the middle of the container/image */
.container .btn {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

</style>
