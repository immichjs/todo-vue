<template>
    <transition name="slide-fade">
        <div
            class="fixed inset-0 flex items-center justify-center overlay bg-gray-line"
            v-if="modalProp"
        >
            <div class="relative flex flex-col items-center w-full max-w-md p-10 text-center bg-gray-200 rounded-md shadow-lg">
                <img src="@/assets/cancel.svg" alt="Icone de aviso" width="30">
                <strong class="mt-1 text-2xl text-text">
                    Aviso!
                </strong>
                <p class="font-semibold">
                    É necessário preencher com uma descrição
                </p>
                <button
                    type="button"
                    class="absolute bg-transparent border-0 right-3 top-3 focus:outline-none"
                    @click="changeModal"
                >
                    <img src="@/assets/close.svg" alt="Fechar Modal" width="25">
                </button>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
    props: ['modalProp'],
    methods: {
        changeModal () {
            this.$emit('changeModal')
        }
    }
}
</script>

<style lang="postcss" scoped>
.overlay {
    background-color: rgba(87, 87, 87, 0.8);
}

.slide-fade-enter-active {
	transition: all .3s ease-in;
}

.slide-fade-leave-active {
	transition: all .3s ease-out;
}

.slide-fade-enter, .slide-fade-leave-to {
	transform: translateY(10px);
	opacity: 0;
}
</style>
