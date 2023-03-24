<template>
    <div v-if="running">
        <svg width="10" height="20" viewBox="0 0 10 20" xmlns="http://www.w3.org/2000/svg">
            <rect x="7" width="3" height="20" />
            <rect width="3" height="20" />
        </svg>
    </div>
    <div v-else>
        <svg width="17" height="20" viewBox="0 0 17 20" xmlns="http://www.w3.org/2000/svg">
            <path d="M0 20V0L17 10L0 20Z" />
        </svg>
    </div>
</template>

<script>
export default {
    name: 'Button',
    props: {
        running: {
            title: Boolean
        }
    }
}
</script>
