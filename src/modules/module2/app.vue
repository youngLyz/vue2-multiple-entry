<template>
    <div class="g-doc">
        <nav-component :current="2" />
        <modules :topics="topics" :page="page" />
    </div>
</template>
<script>
import navComponent from '~components/nav-component.vue'
import modules from '~components/module-2.vue'
import api from '~api'
export default {
    name: 'index-app',
    data() {
        return {
            page: Number(new URLSearchParams(window.location.search).get('page')) || 1,
            topics: []
        }
    },
    components: {
        navComponent,
        modules
    },
    async mounted() {
        const { success, data } = await api.get('topics', { page: this.page })
        if (success) this.topics = data
    },
    metaInfo: {
        title: '模块2'
    }
}
</script>
