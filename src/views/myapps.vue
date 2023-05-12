<template>
    <div class="container">
        <div class="container-1">
            <h1>Add Your Tasks</h1>
            <hr>
            <div class="filters">
                <button @click="showCompleted = !showCompleted">
                    {{ showCompleted ? 'Show all' : 'Hide completed' }}
                </button>
            </div>
            <ul>
                <li v-for="kegiatan in filteredKegiatan" :key="kegiatan.id">
                    <div class="kegiatan-info">
                        <div class="kegiatan-list">
                            <input type="checkbox" v-model="kegiatan.completed">
                            <span :class="{ completed: kegiatan.completed }">{{ kegiatan.nama
                            }}
                            </span>
                        </div>
                        <button class="btn-del" @click="deleteKegiatan(kegiatan)">Delete</button>
                    </div>
                </li>
            </ul>
            <form @submit.prevent="addKegiatan">
                <input type="text" v-model="newKegiatan" placeholder="Add a task">
                <button type="submit">Add</button>
            </form>
        </div>
        <p class="creator">Created by <a href="https://www.instagram.com/_mdzakyefendi/" target="_blank">M. Dzaky Efendi</a>
        </p>
    </div>
</template>
    
<script>
export default {
    data() {
        return {
            kegiatanList: [],
            newKegiatan: '',
            showCompleted: false,
        };
    },
    methods: {
        addKegiatan() {
            const newId = this.kegiatanList.length + 1;
            this.kegiatanList.push({
                id: newId,
                nama: this.newKegiatan,
                completed: false,
            });
            this.newKegiatan = '';
        },
        deleteKegiatan(kegiatan) {
            const index = this.kegiatanList.indexOf(kegiatan);
            this.kegiatanList.splice(index, 1);
        },
        toggleCompleted(kegiatan) {
            kegiatan.completed = !kegiatan.completed;
        },
    },
    computed: {
        filteredKegiatan() {
            return this.showCompleted
                ? this.kegiatanList.filter((t) => !t.completed)
                : this.kegiatanList
        },
    },
};
</script>
    
<style scoped>
.container {
    border: 1px solid rgba(255, 255, 255, .5);
    border-radius: 25px;
    backdrop-filter: blur(8px);
}

.container .container-1 {
    margin: 30px;
}

.kegiatan-info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 90%;
    margin-bottom: 5px;
    border-radius: 50px;
}

.kegiatan-info:hover {
    background-color: #6DA9E4;
    transition: 0.2s ease;
}

button {
    background-color: #A8D8EA;
    color: #333;
}

input[type="text"] {
    padding: 10px;
    font-family: Arial, sans-serif;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 50px;
    color: #464545;
    background-color: #AAC4FF;
}

input[type="text"]:focus {
    outline: none;
    border-color: #66afe9;
}

input[type="text"]:hover {
    background-color: #A8D8EA;
}


input[type="checkbox"]::before {
    content: '\2713';
    font-size: 14px;
    position: absolute;
    top: -3px;
    right: -0.px;
    color: #464444;
    visibility: hidden;
}

input[type="checkbox"]:checked::before {
    visibility: visible;
}

input[type="checkbox"] {
    position: relative;
    appearance: none;
    border-radius: 50%;
    width: 15px;
    height: 15px;
    border: 1px solid #ccc;
    background-color: #E4F9F5;
    margin-bottom: -3px;
    top: -2px;
    margin-left: 10px;
}

input[type="checkbox"]:hover {
    border: 2px solid #333;
    transition: 0.5ms;
}

.completed {
    text-decoration: line-through 2px black;
}

.filters {
    margin-bottom: 10px;
}

ul li {
    list-style-type: none;
}

input {
    margin-right: 10px;
}

.creator {
    font-size: smaller;
}

form input {
    border: none;
    border-radius: 3px;
}
</style>
    