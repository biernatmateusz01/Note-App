<template>
    <div @click.self="$emit('close-modal')" class="bg-black h-screen w-screen fixed top-0 left-0 z-50 bg-opacity-70 flex items-center justify-center">
        <slot/>
    </div>
</template>