<template>
    <div v-if="showModal" class="modal">
        <div class="modal-content text-dark">
            <span class="close" @click="closeModal">&times;</span>
            <p>{{ data.price }}</p>
            <p>{{ data.duration }}</p>
            <p>{{ data.plan }}</p>
            <p>{{ data.description }}</p>
        </div>
    </div>
</template>
  
<script>
export default {
    props: {
        data: Object,
    },
    data() {
        return {
            showModal: false,
            duration: null,
        };
    },
    methods: {
        openModal() {
            this.showModal = true;
        },
        closeModal() {
            this.showModal = false;
        },
    },
};
</script>
  
<style scoped>
/* Stile per la modale */
.modal {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
}

.modal-content {
    background-color: #fff;
    padding: 20px;
    width: 70%;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    text-align: center;
}

.close {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 30px;
    font-weight: bold;
    cursor: pointer;
}
</style>
  