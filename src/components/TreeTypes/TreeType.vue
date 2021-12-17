<template>
  <div ref="tree-type">
      <div class='row tree-type-tbtn'>
        <button class='btn btn-secondary'  @click='treePr'>
          <img style="" src="" ref="tree-pr" alt="Read book">Teams</button>
        <button class='btn btn-secondary' @click='treeGr'>
        <img style="" src="" ref="tree-gr" alt="Read book">Groups</button>
        <button class='btn btn-secondary' @click='treeRs'>
          <img style="" src="" ref="tree-rs" alt="Read book">Resources</button>
        <button class='btn btn-secondary' @click='treeDp'>
          <img style="" src="" ref="tree-dp" alt="Read book">Departments</button>
      </div>
      <div class='row tree-type-bbtn'>
        <button class='btn btn-secondary'  @click='treeTe'>
          <img style="" src="" ref="tree-te" alt="">Fighters</button>
        <button style="width: 120px" class='btn btn-secondary'  @click='treeDi'>
          <img style="" src="" ref="tree-di" alt="">Paramedics</button>
        <button style="width: 150px" class='btn btn-secondary'  @click='treeDr'>
          <img  src="" ref="tree-dr" alt="">Communicators</button>
        <button class='btn btn-secondary'  @click='treeTr'>
          <img style="" src="" ref="tree-tr" alt="">Pathfinders</button>
        <button class='btn btn-secondary'  @click='treeAt'>
          <img style="" src="" ref="tree-at" alt="">Launchers</button>
        <button class='btn btn-secondary'  @click='treeVt'>
          <img style="" src="" ref="tree-vt" alt="">Snipers</button>
        <button class='btn btn-secondary'  @click='treeAl'>
          <img style="" src="" ref="tree-al" alt="">Assistants</button>
        <button class='btn btn-secondary'  @click='treeBl'>
          <img style="" src="" ref="tree-bl" alt="">Bombers</button>
        <button class='btn btn-secondary'  @click='treeIi'>
          <img style="" src="" ref="tree-ii" alt="">Codes</button>
      </div>
  </div>
</template>

<script>
import eventBus from '../../event-bus'
import axios from 'axios'
import xml2js from 'xml2js'

export default {
  name: 'TreeType',
  async mounted () {
    let ref = this
    axios.get('assets/globalparametrs.xml').then(async (response) => {
      console.log('response', response)
      let globalData = await this.parseXML(response.data)
      console.log('getdatatype', globalData)
      ref.defineTreeButtons(globalData.DD.Datadef.Tree)
    })
  },
  methods: {
    parseXML (data) {
      return new Promise((resolve) => {
        const parser = new xml2js.Parser({ explicitArray: false })
        parser.parseString(data, function (err, result) {
          resolve(result)
          if (err) {
            throw err
          }
        })
      })
    },
    defineTreeButtons: function (trees) {
      // console.log(this.$refs['tree-pr'].parentElement)
      let baseUrl = 'assets/img/treeTypeIcons/'
      trees.forEach(tree => {
        // console.log('url', `${baseUrl}${tree.icon}`)
        if (tree.key === 'Pr') {
          this.$refs['tree-pr'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-pr'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'Gr') {
          this.$refs['tree-gr'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-gr'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'Dp') {
          this.$refs['tree-dp'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-dp'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'Rs') {
          this.$refs['tree-rs'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-rs'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'al') {
          this.$refs['tree-al'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-al'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'at') {
          this.$refs['tree-at'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-at'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'bl') {
          this.$refs['tree-bl'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-bl'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'di') {
          this.$refs['tree-di'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-di'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'dr') {
          this.$refs['tree-dr'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-dr'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'ii') {
          this.$refs['tree-ii'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-ii'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'te') {
          this.$refs['tree-te'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-te'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'tr') {
          this.$refs['tree-tr'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-tr'].parentElement.innerHTML = tree.Title
        } else if (tree.key === 'vt') {
          this.$refs['tree-vt'].src = `${baseUrl}${tree.icon}`
          // this.$refs['tree-vt'].parentElement.innerHTML = tree.Title
        }
      })
      // console.log('definceTreebuttons', trees)
    },
    treePr: function () {
      eventBus.$emit('treePr')
    },
    treeGr: function () {
      eventBus.$emit('treeGr')
    },
    treeRs: function () {
      eventBus.$emit('treeRs')
    },
    treeDp: function () {
      eventBus.$emit('treeDp')
    },
    treeTe: function () {
      eventBus.$emit('treeTe')
    },
    treeDi: function () {
      eventBus.$emit('treeDi')
    },
    treeDr: function () {
      eventBus.$emit('treeDr')
    },
    treeTr: function () {
      eventBus.$emit('treeTr')
    },
    treeAt: function () {
      eventBus.$emit('treeAt')
    },
    treeVt: function () {
      eventBus.$emit('treeVt')
    },
    treeAl: function () {
      eventBus.$emit('treeAl')
    },
    treeBl: function () {
      eventBus.$emit('treeBl')
    },
    treeIi: function () {
      eventBus.$emit('treeIi')
    }
  }

}

</script>

<style >
.tree-type-tbtn> button {
  width: 12%;
  margin: 3px;
  padding: 5px 10px 5px 0px;
  color: white;
}
.tree-type-bbtn> button {
  height: 40px;
  width: 10%;
  color: white;
  margin: 3px;
  padding: 0px 0px 0px 0px;
}
.tree-type-tbtn> button> img {
  width:50px;
  height: 30px;
}
.tree-type-bbtn> button> img {
  width:30px;
  height: 25px;
}
</style>
