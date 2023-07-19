<template>
    <div class="card">
        <div class="card-header">
            <p>{{ name }}</p>
            <button @click="removeTask(id)">remove</button>
        </div>
    </div>
</template>

<script>
export default {
    props: ['name','id'],
    methods: {
        removeTask(id) {
            this.$emit('removeTask', id);
        },
    },
};
</script>
