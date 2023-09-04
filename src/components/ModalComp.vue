<template>
    <div v-if="showModal" class="modal">
        <div class="modal-content text-dark p-0">
            <div class="logo-brand d-flex align-items-center justify-content-center modal-nav">
                <i class="fa-brands fa-spotify display-4"></i>
                <h3 class="fw-semibold ps-1">Spotify</h3>
            </div>
            <div class="d-flex flex-column align-items-center justify-content-center">
                <span class="fw-semibold display-3">${{ data.price }}</span>
                <span>{{ data.duration }}</span>
            </div>
            <!--button colseModal-->
            <div class="close" @click="closeModal">
                <div class="d-flex justify-content-center align-items-center w-100 h-100"
                    style="border-radius:50%; font-size: 15px;">
                    <i class="fa-solid fa-x"></i>
                </div>
            </div>
            <!--section with data announcement-->
            <section class="d-flex flex-column align-items-start justify-content-center px-4">
                <div>
                    <h4 class="pb-4">Includes</h4>
                    <ul>
                        <li><i class="fa-solid fa-circle"></i><span class="ps-1">{{ data.plan }}</span></li>
                        <li><i class="fa-solid fa-circle"></i><span class="ps-1">{{ data.description }}</span></li>
                        <li><i class="fa-solid fa-circle"></i><span class="ps-1">{{ data.contract }}</span></li>
                    </ul>
                </div>
            </section>
            <div class="d-flex align-items-center flex-column justify-content-center pb-5">
                <button class="btn btn-subscribe rounded-5 fw-semibold px-5">Subscribe</button>
                <p class="py-4 fw-semibold" style="color: #75ced9;">Or $9.90 {{ data.duration }} without contract</p>

            </div>

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
  
<style lang="scss" scoped>
@use '../assets/partials/variables' as *;

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
    width: 30%;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    border-radius: 0;
    border: 10px solid transparent;
    background-clip: padding-box;
    /* Assicura che il gradiente non si estenda oltre il padding */
    border-image: linear-gradient(to right, #4b443a 10%, #4b443a 10%);
    border-image-slice: 1;

}



.close {
    position: absolute;
    top: -30px;
    right: -28px;
    font-size: 15px;
    font-weight: bold;
    cursor: pointer;
    background-color: $white;
    color: rgb(22, 207, 22);
    width: 40px;
    height: 40px;
    text-align: center;
    border-radius: 50%;
}

.modal-nav {
    background-color: rgb(22, 207, 22);
    color: $white;
}

ul {
    padding: 0;
    list-style: none;

    li {
        padding-bottom: 15px;

        i {
            font-size: 8px;
        }
    }
}

.btn-subscribe {
    background-color: red;
    color: $white;
}
</style>
  