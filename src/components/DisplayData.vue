<template>
    <div class="center">
        <div class="main">
            <div v-if="loaded">
                <div class="entry">
                    <div class="title">Cases overall</div>
                    <div class="data">{{cases}}</div>
                </div>
                <div class="entry">
                    <div class="title">Cases today</div>
                    <div class="data">{{todayCases}}</div>
                </div>
                <div class="entry">
                    <div class="title">Deaths overall</div>
                    <div class="data">{{deaths}}</div>
                </div>
                <div class="entry">
                    <div class="title">Deaths today</div>
                    <div class="data">{{todayDeaths}}</div>
                </div>
                <div class="entry">
                    <div class="title">Recovered overall</div>
                    <div class="data">{{recovered}}</div>
                </div>
                <div class="entry">
                    <div class="title">Recovered today</div>
                    <div class="data">{{todayRecovered}}</div>
                </div>
            </div>
            <div v-else class="spinner">Loading ...</div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'DisplayData',
    data() {
        return {
            loaded: false,
            cases: Number,
            deaths: Number,
            recovered: Number,
            todayCases: Number,
            todayDeaths: Number,
            todayRecovered: Number
        }
    },
    props: {
        global: Boolean
    },
    watch: {
        global() {
            this.loaded = false;
            this.fetchData();
        }
    },
    mounted() {
        this.fetchData();
    },
    methods: {
        fetchData() {
            fetch(`https://disease.sh/v3/covid-19/${this.global ? "all" : "countries/poland?strict=true"}`)
            .then(res => res.json())
            .then(data => {
                this.cases = data.cases;
                this.deaths = data.deaths;
                this.recovered = data.recovered;
                this.todayCases = data.todayCases;
                this.todayDeaths = data.todayDeaths;
                this.todayRecovered = data.todayRecovered;
                this.loaded = true;
            })
            .catch(console.error);
        }
    }
}
</script>

<style scoped>
.center {
    width: 100%;
    display: flex;
    justify-content: center;
}

.main {
    margin-top: 50px;
    width: calc(100% - 50px);
    height: 100vh;
    max-width: 600px;
    max-height: 700px;
    box-sizing: border-box;
    border: 1px solid #FFF;
    border-radius: 10px;
    position: relative;
}

.spinner {
    text-align: center;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 40px;
}

.entry {
    height: 110px;
    display: flex;
    align-items: center;
}

.title {
    font-weight: 700;
    font-size: 28px;
    margin-right: 20px;
    margin-left: 40px;
}

.data {
    font-size: 24px;
}
</style>