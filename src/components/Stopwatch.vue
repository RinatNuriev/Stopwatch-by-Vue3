<template>
    <div class="box">
        <div class="box__time " :class="{ boxActive: running }">
            <div class="time__hour" v-show="hours">{{ hours }}</div>
            <div class="time__minute" v-show="minutes">{{ minutes }}</div>
            <div class="time__second">{{ seconds }}</div>
        </div>
        <div class="hr" :class="{ hrActive: running }"></div>
        <div class="box__controls" :class="{ controlsActive: running }">
            <div @click="start" class="controls-pause">
                <Button :running="running" />
            </div>
            <div @click="reset" class="controls-stop"><svg width="20" height="20" viewBox="0 0 20 20"
                    xmlns="http://www.w3.org/2000/svg">
                    <rect width="20" height="20" />
                </svg></div>
        </div>

    </div>
</template>

<script>
import Button from './UI/Button.vue'

export default {
    name: "Stopwatch",
    components: { Button },
    data() {
        return {
            seconds: null,
            minutes: null,
            hours: null,
            isActive: false,
            timeBegan: null,
            timeStopped: null,
            stoppedDuration: 0,
            started: null,
            running: false,
        };
    },
    methods: {
        clockRunning() {
            let currentTime = new Date(), 
            timeElapsed = new Date(currentTime - this.timeBegan - this.stoppedDuration)
            this.hours = timeElapsed.getUTCHours();
            this.minutes = timeElapsed.getUTCMinutes();
            this.seconds = timeElapsed.getUTCSeconds();

        },
        start() {
            if (this.running) {
                this.running = false;
                this.timeStopped = new Date();
                clearInterval(this.started);
                return;
            }
            if (this.timeBegan === null) {
                this.reset();
                this.timeBegan = new Date();
            }
            if (this.timeStopped !== null) {
                this.stoppedDuration += (new Date() - this.timeStopped);
            }
            this.started = setInterval(this.clockRunning, 10);
            this.running = !this.running;
        },
        reset() {
            this.running = false;
            clearInterval(this.started);
            this.stoppedDuration = 0;
            this.timeBegan = null;
            this.timeStopped = null;
            this.seconds = null;
            this.minutes = null;
            this.hours = null;
        },
    },

}
</script>

<style scoped>
.box {
    width: 225px;
    height: 120px;
    background: #696969;
    color: #9E9E9E;
    fill: #9E9E9E;
    position: relative;
}

.boxActive {
    color: white;
    fill: white;
}

.box__time {
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 400;
    font-size: 22px;
    line-height: 21px;
    height: 50%;

}

.time__hour {
    width: 20px;
    text-align: right;
}

.time__hour::after {
    content: ':';
}

.time__minute {
    width: 20px;
    text-align: right;
}

.time__minute::after {
    content: ':';
}

.time__second {
    width: 20px;
    text-align: right;
}

.colon {
    width: 20px;
    text-align: center;
}

.hr {
    border: 1px solid #9E9E9E;
    width: 100%;
    position: absolute;
}

.hrActive {
    border: 1px solid white;
}

.box__controls {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50%;

}

.controlsActive {
    fill: white;
}

.controls-pause {
    margin-right: 48px;
    cursor: pointer;

}

.controls-stop {
    cursor: pointer;

}
</style>