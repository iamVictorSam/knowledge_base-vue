
<template>

    <div class="card">
        <div class="wrapper">
            <div class="timeDiv">
                <div class="green">{{ value.answered_by }}</div>
                <span>{{ value.answered_on.slice(0, 10) }}</span>
            </div>
            <h2>{{ value.question }}</h2>
            <p v-html="value.answer"></p>
        </div>
    </div>



</template>

<script >


export default {
    data() {
        return {
            value: null,
        };

    },

    created() {
        var resp = this.$route.query.post
        this.value =
            JSON.parse(resp);
        console.log(this.value.question)
    },

}

</script>

<style lang="scss">
html,
body {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    margin-top: 16px;
    margin-bottom: 16px;
}

div#app {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;

    .search-wrapper {
        position: relative;

        label {
            position: absolute;
            font-size: 18px;
            color: rgba(0, 0, 0, 0.5);
            top: 8px;
            left: 2px;
            z-index: -1;
            transition: 0.15s all ease-in-out;
        }

        input {
            padding: 20px 12px;
            margin-bottom: 30px;
            width: 600px;
            color: rgba(0, 0, 0, 0.7);
            border: 1px solid rgba(0, 0, 0, 0.12);
            border-radius: 20px;
            transition: 0.15s all ease-in-out;
            background: white;
            font-size: 18px;

            &:focus {
                outline: none;
                transform: scale(1.5);

                &+label {
                    font-size: 18px;
                    font-weight: bold;
                    transform: translateY(-55px) translateX(-122px);
                }
            }

            &::-webkit-input-placeholder {
                font-size: 18px;
                color: rgba(0, 0, 0, 0.5);
                font-weight: 100;
            }
        }
    }

    .title {
        color: black;
        padding-bottom: 30px;
    }

    .wrapper {
        display: flex;
        /* max-width: 854px; */
        flex-direction: column;
        flex-wrap: wrap;
        padding-top: 12px;
        text-align: start;
    }

    .card {
        background-color: black;
        border-radius: 10px;
        padding: 60px;
        box-shadow: rgba(0, 0, 0, 0.117647) 0px 4px 10px,
            rgba(0, 0, 0, 0.117647) 0px 1px 4px;
        width: 800px;
        margin: 20px;
        transition: 0.15s all ease-in-out;

        &:hover {
            transform: scale(1.1);
        }

        a {
            text-decoration: none;
            padding: 12px;
            color: #03a9f4;
            font-size: 24px;
            display: flex;
            flex-direction: column;
            align-items: center;

            img {
                height: 100px;
            }

            small {
                font-size: 10px;
                padding: 4px;
            }
        }
    }

    .timeDiv {
        display: flex;
        justify-content: space-between;
    }

    .hotpink {
        background: hotpink;
    }

    .green {
        padding: 0 7px;
        text-align: center;
        border-radius: 10px;
        background: green;
        font-weight: bold;
    }

    .box {
        width: 100px;
        height: 100px;
        border: 1px solid rgba(0, 0, 0, 0.12);
    }
}
</style>
