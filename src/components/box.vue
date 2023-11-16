<template>
    <div class="app">
        <div ref="open" @click="open" v-if="!on" class="open">
            <i class="fi fi-rr-comments"></i>
        </div>
        <div v-if="on" class="box">
            <div :class="'top ' + screen">
                <i class="fi fi-rr-cross-circle close" @click="on = !on"></i>
                <h3>{{ screen }}</h3>
                <h5 v-if="screen != 'messages'">{{ name }}</h5>

                <div v-if="screen == 'messages'" class="peoples">
                    <img :src="chatImg" alt="chatImg" />
                </div>
            </div>
            <div class="bottom">
                <i @click="screen = 'home'" class="fi fi-rr-home"></i>
                <i
                    @click="screen = 'messages'"
                    class="fi fi-rr-comment-alt-middle"
                ></i>
                <i
                    v-if="FAQ != '{}' && FAQo"
                    @click="screen = 'questions'"
                    class="fi fi-rr-question-square"
                ></i>
            </div>
            <div v-if="screen == 'questions'" class="FAQ">
                <div class="Fwrapper">
                    <div dir="rtl" v-for="key of FAQo" class="FBox">
                        {{ key[0] }}<br />
                        {{ key[1] }}
                    </div>
                </div>
            </div>
            <div class="home_" v-if="screen == 'home'">
                <img src="../static/logo.jpg" class="logo" />
                {{ description }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ChBox",
    props: {
        fetchURL: {},
        description: {},
        logo: {},
        name: {
            default: "",
        },

        chatImg: {
            default: "https://cdn-icons-png.flaticon.com/512/149/149071.png",
        },

        FAQ: {
            default: "",
        },
    },
    data() {
        return {
            FAQo: JSON.parse(this.FAQ),
            screen: "home",
            on: false,
        };
    },
    methods: {
        open() {
            this.$refs.open.style.transformOrigin = "100% 100%";
            this.$refs.open.style.borderRadius = "20px";
            this.$refs.open.style.transform = "scale(1)"
            this.$refs.open.style.width = "400px";
            this.$refs.open.style.height = "550px";
            this.screen = "home";
            setTimeout(() => {
                this.on = !this.on;
                this.$refs.open.style = "";
            }, 1500);
        },
    },
};
</script>

<style scoped>
.home_ {
    width: 100%;
    padding: 5px 30px;
    box-sizing: border-box;
    text-align: center;
    margin-top: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    justify-content: space-around;
}
.box {
    width: 400px;
    height: 550px;
    position: fixed;
    bottom: 5px;
    right: 15px;
    box-shadow: 0 0 4px #25252541;
    overflow: hidden;
    background-color: white;
    border-radius: 20px;
}
.top {
    background-color: #6e6eff;
    color: white;
    width: 100%;
    height: 100px;
    display: flex;
    align-items: center;
    position: relative;
    top: 0;
    justify-content: center;
    flex-direction: column;
    row-gap: 10px;
}
.messages {
    height: 60px;
}
.close {
    font-size: 2rem;
    position: absolute;
    top: 10px;
    left: 10px;
    cursor: pointer;
}
.messages h5,
.messages h3 {
    transform: scale(0.7);
}
.top h3 {
    font-size: 2rem;
}
.bottom {
    background-color: #5757ff;
    color: white;
    width: 100%;
    height: 50px;
    font-size: 1.7rem;
    display: flex;
    position: absolute;
    bottom: 0;
    align-items: center;
    justify-content: space-evenly;
    column-gap: 10px;
}
.bottom i {
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}
.bottom i:hover {
    transform: scale(0.93);
    opacity: 0.9;
}
.peoples {
    position: absolute;
    top: 10px;
    right: 20px;
}
.logo {
    width: 150px;
    border-radius: 100px;
}
.peoples img {
    width: 40px;
}
.search {
    width: 100%;
    display: flex;
    align-items: center;
    padding: 10px;
    font-size: 1.6rem;
    column-gap: 20px;
    justify-content: center;
}
.search i {
    transition: all 0.3s;
}
input {
    border-radius: 5px;
    font-size: 1.2rem;
    padding: 5px;
    width: 80%;
    outline: 0;
    border: 0;
    background-color: #d8d8d8;
    color: #1f1f1f;
}
.Fwrapper {
    width: 100%;
    display: flex;
    margin-top: 10px;
    justify-content: center;
    gap: 20px;flex-wrap: wrap;
}
.FBox {
    width: 80%;
    background: #ffaf46;
    padding: 20px;
    color: white;
    border-radius: 10px;
}
input:not(::placeholder) {
    background-color: white;
    border: 1px solid gray;
}
.open {
    width: 50px;
    height: 50px;
    background: #7746ff;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 100px;
    position: fixed;
    bottom: 10px;
    right: 10px;
    font-size: 2rem;
    cursor: pointer;
    box-shadow: 3px 3px 5px #0000005c;
    transition: all 0.3s;
}
.open:hover {
    transform: scale(1.1);
}
</style>
