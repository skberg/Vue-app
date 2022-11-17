
<template>
    <div class="fetch">
        <div>
            <input type="text" class="SerchFeild" v-model="search" placeholder="Søk eks. 22:00 eller Under" />
    
        </div>
    
        <button type="button" class="Savebutton" @click="saveFile()">Lage rapport</button>
    
        <br />
        <br />
    
        <div class="CardHolder">
            <div v-for="Movi in  filterMovies" :key="Movi.id">
                <div class="buttonWen"> {{ Movi.schedule.time }} {{ Movi.schedule.days[0] }}</div>
    
                <div class="card" :id="Movi.id">
                    <img :src="Movi.image.medium" />
    
    
                    <div class="info">
                        <div class="TopInfoHolder">
    
                            <p class="Rating">
                                <span class="RoundRating">{{ Movi.rating.average }}</span> rating
                            </p>
                            <input type="checkbox" id="scales" :value="Movi.name" v-model="dataSe.MovieSelected" @click="log($event)" name="scales" class="chekbox" />
                        </div>
                        <br />
    
                        <div class="content">
    
                            <p class="tittle">{{ Movi.name }}</p>
    
                            <p> <span class="carbutton">{{ Movi.genres[0] }}</span> <span class="spascer"> | </span><span class="carbutton">{{ Movi.genres[2] }}</span>
                                <span class="spascer"> | </span> <span class="carbutton">{{ Movi.genres[1] }}</span>
                            </p>
    
    
    
                            <div class="Tekst">
    
                                <h5 v-if="Movi.summary.length < 100"> {{ Movi.summary.replace(/(<([^>]+)>)/gi, "") }}</h5>
                                <h5 v-if="Movi.summary.length >= 100"> {{ Movi.summary.replace(/(<([^>]+)>)/gi, "").substring(0, 100) + ".." }} <span class="ShowMore" @click='toggle = !toggle === Movi.id && toggle !== null ? null : Movi.id'>
                                click here </span></h5>
    
                                <h5 id="hide" v-if="toggle && toggle === Movi.id">{{ Movi.summary.replace(/(<([^>]+)>)/gi, "") }}</h5>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>





<script>
export default {


    data() {
        return {

            Movie: [],
            search: '',
            dataSe: {
                MovieSelected: [],
            },
            toggle: false,



            saveFile() {
                if (this.dataSe.MovieSelected.length === 0) {
                    alert('Failed to save the file! please select a movie');
                    a.dispatchEvent('')
                } else {
                    const test = this.dataSe.MovieSelected;
                    const blob = new Blob([test], { type: 'text/plain' })
                    const e = document.createEvent('MouseEvents'),
                        a = document.createElement('a');
                    a.download = "Movis.txt";
                    a.href = window.URL.createObjectURL(blob);
                    a.dataset.downloadurl = ['text/txt', a.download, a.href].join(':');
                    e.initEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
                    a.dispatchEvent(e);

                }
            },
        }
    },

    mounted() {
        fetch('https://api.tvmaze.com/show/')
            .then(res => res.json())
            .then(data => this.Movie = data.slice(0, 60)

            )
            .catch(err => console.log(err.message))



    },
    computed: {
        filterMovies: function() {
            return this.Movie.filter((Movi) => {
                return Movi.name.match(this.search) || Movi.schedule.time.match(this.search);
            })
        },



    }


}
</script>







<style scoped>
.fetch {
    background-color: #1e1e1e;
    padding: 10px;
    border-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 1px 3px 0px, rgba(0, 0, 0, 0.06) 0px 1px 2px 0px;
    width: max-content;
}

.topholder {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    max-width: max-content;
    grid-gap: 1px;
    margin: 1px auto;
}

.TopInfoHolder {
    display: grid;
    grid-template-columns: 1fr auto;
    margin-bottom: 55px;
    margin: 15px;
}

.CardHolder {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;
    margin: auto;
    position: relative;
    left: 50%;
    transform: translate(-50%, -0%);
}

.card {
    display: grid;
    grid-template-columns: auto 1fr;
    grid-gap: 15px;
    z-index: 1;
    margin: 10px auto;
    background-color: #5a8fa35b;
    padding: 5px;
    border: #609d9f 3px solid;
    border-radius: 5px;
}

.tittle {
    color: white;
    border-bottom: #609d9f 2px solid;
    font-size: 20px;
    margin-bottom: 5px;
    font-weight: 700;
}

p {
    color: white;
}

.spascer {
    color: #609d9f;
    font-weight: 500;
}

.Img {
    border-radius: 5px;
}

.carbutton {
    background-color: #355c5e;
    padding-left: 10px;
    padding-right: 10px;
    padding-bottom: 2px;
    margin-top: 50px;
    border-radius: 50px;
}

.Rating {
    margin-left: -16px;
}

.RoundRating {
    background-color: #355c5e;
    padding-top: 4px !important;
    padding-bottom: 5px;
    padding-left: 5px;
    padding-right: 5px;
    margin: auto;
    border-radius: 90%;
    text-align: center;
}

.SerchFeild {
    margin: auto;
    background-color: transparent;
    border: 3px solid #609d9f;
    padding: 10px;
    position: relative;
    left: 50%;
    transform: translate(-50%, -0%);
    width: 300px;
    border-radius: 50px;
    color: white;
    font-size: 15px;
}

.buttonholder {
    float: right;
    margin-bottom: 50px;
}

.buttonWen {
    background-color: #609d9f;
    position: absolute;
    left: 0px;
    top: -11px;
    z-index: -1;
    width: max-content;
    padding-left: 5px;
    padding-right: 5px;
    padding-bottom: 1px;
    border-radius: 5px 5px 0px 0px;
    font-size: 14px;
    color: white;
}

.info {
    width: 100%;
}

.Tekst {
    margin-top: 15px;
    max-width: fit-content;
    color: rgba(235, 235, 235, 0.64);
}

.chekbox {
    background-color: transparent;
}

.Savebutton {
    background-color: #355c5e;
    color: aliceblue;
    padding: 8px;
    border: none;
    border-radius: 5px;
}

.ShowMore {
    font-size: 10px;
    background-color: transparent;
    border: none;
    border-bottom: #609d9f 1px solid;
    color: whitesmoke;
    cursor: pointer;
}

@media only screen and (max-width: 45em) {
    .CardHolder {
        display: grid;
        grid-template-columns: 1fr;
    }
}
</style>
