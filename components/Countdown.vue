<template>
    <section :class="this.countdownColor" class="text-6xl">
        <div class="mr-6 relative">
            {{ days }}
            <div class="label text-sm absolute bottom">days</div>
        </div>
        <div class="mr-6 relative">
            {{ hours }}
            <div class="label text-sm absolute bottom">hours</div>
        </div>
        <div class="mr-6 relative">
            {{ minutes }}
            <div class="label text-sm absolute bottom">min</div>
        </div>
        <div class="relative">
            {{ seconds }}
            <div class="label text-sm absolute bottom">sec</div>
        </div>
    </section>
</template>

<script>
    export default {
        name: "Countdown",

        data() {
            return {
                days: 0,
                hours: 0,
                minutes: 0,
                seconds: 0,
            };
        },
        computed: {
            countdownColor() {
                if (this.days < 7) {
                    return "text-orange-500";
                } else if (this.days < 4) {
                    return "text-green-500";
                } else if (this.days < 7) {
                    return "text-green-700";
                } else {
                    return "text-gray-500";
                }
            },
            _seconds: () => 1000,
            _minutes() {
                return this._seconds * 60;
            },
            _hours() {
                return this._minutes * 60;
            },
            _days() {
                return this._hours * 24;
            },
        },

        mounted() {
            this.showRemaining();
        },

        methods: {
            showRemaining() {
                const timer = setInterval(() => {
                    // const eta = new Date(
                    //     Date.UTC(2021, 11, 3, 18, 30, 0, 0)
                    // ).getTime();

                    const eta = new Date(
                        Date.UTC(2022, 2, 25, 22, 50, 0, 0)
                    ).getTime();

                    const now = new Date().getTime();

                    var distance = eta - now;
                    this.days = Math.floor(distance / this._days);
                    this.hours = Math.floor((distance % this._days) / this._hours);
                    this.minutes = Math.floor(
                        (distance % this._hours) / this._minutes
                    );
                    this.seconds = Math.floor(
                        (distance % this._minutes) / this._seconds
                    );


                    // If the count down is finished, write some text
                    if (distance < 0) {
                        this.$emit("arrived");
                    }
                }, 1000);
            },
        },
    };
</script>

<style>
</style>
