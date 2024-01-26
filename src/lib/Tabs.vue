<template>
    <div>
        <div v-for="(t,index) in titles" :key="index">{{ t }}</div>    
        <!-- <component :is="xxx">表示动态切换要渲染的组件 -->
        <component v-for="(c,index) in defaults" :is="c" :key="index" />
    </div>
</template>

<script lang="ts">
import Tab from './Tab.vue'
export default { 
    components: {
        Tab
    },
    setup(props, context) {
        const defaults = context.slots.default()
        defaults.forEach((tag)=> {
            if(tag.type !== Tab){
                throw new Error('Tabs 子标签必须是 Tab')
            }
        })
        const titles = defaults.map((tag) => {
            return tag.props.title
        })
        return {
            defaults, titles
        }
    }
}
</script>