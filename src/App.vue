<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Animations</h1>
                <hr>
                <button class="btn btn-primary" v-on:click="show=!show">Show Alert</button>
                <br><br>

                <select v-model="animationClass" class="form-control">
                    <option value="fade">fade</option>
                    <option value="slide">slide</option>
                </select>

                <transition v-bind:name="animationClass" mode="out-in">
                    <div class="alert alert-info" v-if="show" key="info">This is info</div>
                    <div class="alert alert-warning" key="warning" v-else>This is info</div>
                </transition>

                <hr>
                <transition name="slide" type="animation" appear>
                    <div class="alert alert-info" v-if="show">This is info</div>
                </transition>

                <transition enter-active-calss="animated bounce" leave-active-class="animated shake">
                    <div class="alert alert-info" v-if="show">This is info</div>
                </transition>
                <hr>
                <hr>

                <button class="button button-primary" @click="load=!load">Load/Remove element</button>
                <br><br>
                <transition @before-enter="beforeEnter"
                            @enter="enter"
                            @after-enter="afterEnter"
                            @after-enter-cancelled="afterEnterCancelled"
                            @before-leave="beforeLeave"
                            @leave="leave"
                            @after-leave="afterLeave"
                            @after-leave-cancelled="afterLeaveCancelled"
                            :css="false">
                    <div style="width:100px; height:100px; background-color: lightcoral"
                         v-if="load"></div>
                </transition>

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                show:true,
                animationClass:'',
                load:true,
            }
        },
        methods:{
            beforeEnter(el){
                console.log('beforeEnter');
            },
            enter(el, done){
                console.log('enter');
                done();
            },
            afterEnter(el){
                console.log('afterEnter');
            },
            afterEnterCancelled(el){
                console.log('afterEnterCancelled');
            },
            beforeLeave(el){
                console.log('beforeLeave');
            },
            leave(el, done){
                console.log('leave');
                done();
            },
            afterLeave(el){
                console.log('afterLeave');
            },
            afterLeaveCancelled(el){
                console.log('afterLeaveCancelled');
            }
        }
    }
</script>

<style>
.fade-enter{
    opacity: 0;
}
.fade-enter-active{
    transition: opacity 1s;
}
.fade-leave{

}
.fade-leave-active{
    transition: opacity 1s;
    opacity: 0;
}

.slide-enter{
    /*transform:translateY(20px);*/
    opacity: 0;
}
.slide-enter-active{
    animation: slide-in 1s ease-out forwards;
    transition: opacity 0.5s;
}
.slide-leave{

}
.slide-leave-active{
    animation: slide-out 1s ease-out forwards;
    transition: opacity 3s;
    opacity: 0;
}
@keyframes slide-in {
    from{
        transform:translateY(20px);
    }
    to{
        transform:translateY(0px);
    }
}
@keyframes slide-out {
    from{
        transform:translateY(0px);
    }
    to{
        transform:translateY(20px);
    }
}
</style>
