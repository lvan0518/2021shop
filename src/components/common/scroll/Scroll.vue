<template>
    <div class="scroll_wrapper" ref="scrollDev">
        <div class="content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    import bs from 'better-scroll'
    export default {
        name: "Scroll",
        props:{
            probeType:{
                type:Number,
                default() {
                    return 0
                }
            }
        },
        data() {
            return {
                scrollDev:null
            }
        },
        mounted() {
            this.scrollDev = new bs(this.$refs.scrollDev,{
                click:true,
                probeType: this.probeType
            })
            this.scrollDev.on('scroll',(pos) => {
                // console.log(pos);
                this.$emit('scroll',pos)
            } )
        },
        methods:{
            scrollTo(x,y,time=300) {
                this.scrollDev.scrollTo(x,y,time);
            }
        }
    }
</script>

<style scoped>

</style>