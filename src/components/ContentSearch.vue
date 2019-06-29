<template>
  <div class='table' id='tableSearch'>
    <h1>{{ msg }}</h1>
    <table>
      <thead>
        <tr>
          <td colspan='4'>
            <field-search @git-search='gitSearch'/>
          </td>
        </tr>
        <tr>
          <th>Name</th>
          <th>Description</th>
          <th>Url</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
          <list v-for='(data,index) in gitList' :key='index' 
          :data='data' 
          :index='index'
          @remove-item='removeField'/>
      </tbody>
    </table>
  </div>
</template>

<script>
import List from './List'
import FieldSearch from './FieldSearch'

export default {
  name: 'contentSearch',
  components: {
    List,
    FieldSearch
  },
  data () {
    return {
      msg: 'Git List',
      query: 'vue',
      resultsCount: 10,
      urlApi: 'https://api.github.com/search/repositories?',
      gitList: []
    }
  },
  beforeMount () {
    this.getData()
  },
  methods: {
    getUrl: function () {
      return `${this.urlApi}q=${this.query}&per_page=${this.resultsCount}`
    },
    writeData ({ items }) {
      this.gitList = items.map(elem => {
        return {
          name: elem.name,
          description: elem.description,
          homepage: elem.html_url
        }
      })
    },
    getData () {
      return fetch(this.getUrl())
        .then(e => e.json())
        .then(e => this.writeData(e))
        .catch(error => console.error(error))
    },
    gitSearch: function (el) {
      this.query = el
      if (el) {
        this.getData()
      }
    },
    removeField (item) {
      this.gitList.splice(item, 1)
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style>
* {
  box-sizing: border-box;
}
body {
  margin: 2em;
}
table {
  border-top: 1px solid #ddd;
  border-collapse: collapse;
  border-spacing: 0;
  width: 100%;
}
table thead td {
  background-color: #e1e7ee;
}
table th,
table td {
  border-bottom: 1px solid #ccc;
  line-height: 1.2;
  text-align: left;
  padding: 0.5rem;
}
table th {
  background: #f5f7fb;
  font-size: 0.8em;
  letter-spacing: 1px;
  text-transform: uppercase;
}
input[type='text'] {
  width: 100%;
  padding: 0.3rem;
}
input[type='submit'],
button {
  border: 1px solid #a6a6a6;
  border-radius: 50%;
  background-color: transparent;
  cursor: pointer;
  font-size: 12px;
  font-weight: normal;
  height: 20px;
  width: 20px;
  padding: 0;
}
input[type='submit']:hover,
button:hover {
  border-color: #df4a12;
}
.actions {
  text-align: right;
  white-space: nowrap;
  width: 80px;
}
.box {
  margin-top: 1em;
  padding: 1em;
  background: #eee;
}
textarea {
  font-family: monospace;
  font-size: 12px;
  margin: 0.5em 0 0 0;
  padding: 0.5em;
  width: 100%;
}
.hidden {
  display: none;
}
</style>
