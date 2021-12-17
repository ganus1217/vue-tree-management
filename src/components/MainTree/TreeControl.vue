<template>
  <div >
    <div class="card"  id='hole-tree'>
      <div class="card-header" id='tree-body-header' style="padding: 0">
        <nav class='navbar navbar-expand-sm navbar-dark bg-secondary'>
          <div class='container-fluid'>
            <a class='navbar-brand' href='javascript:void(0)'>+</a>
            <button class='navbar-toggler' type='button' data-bs-toggle='collapse' data-bs-target='#mynavbar'>
              <span class='navbar-toggler-icon'></span>
            </button>
            <div class='collapse navbar-collapse' id='mynavbar'>
              <ul class='navbar-nav me-auto'>
                <li class='nav-item'>
                  <a class='nav-link' href='javascript:void(0)'>code</a>
                </li>
              </ul>
              <form class='d-flex'>
                <button class='btn btn-secondary nav-link' style='margin:2px' type='button'>Filter</button>
                <input class='form-control me-2' id='mySearch' type='text' style='width:330px;border-radius:17px;
                height:40px;margin-top: 2px;' placeholder='Search' v-bind:search='value' @keyup='searchFunc($event.target.value)'>
              </form>
            </div>
          </div>
        </nav>
      </div>
      <div class="card-body" id='tree-body-body' style='overflow:auto;'>
          <Tree
            id='my-tree-id'
            ref='my-tree'
            :custom-options='myCustomOptions'
            :custom-styles='myCustomStyles'
            :nodes='treeDisplayData'
          ></Tree>
      </div>
    </div>
    <div id='tree-control'>
      <div class='row' id='tree-control-set'>
        <div class='col-sm-2' style="margin-left:-40px;">
          <fieldset>
            <label for=''>Type</label><br>
            <img ref="icon-type" src='assets/img/treeTypeIcons/te.jpg' width='30px'>
          </fieldset>
        </div>
        <div class='col-sm-1' style="margin-top: -3px;">
          <fieldset>
            <label for=''>Sort Code</label><br>
            <input style="width:70px" ref="sort-cord" type='text' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <img src="assets/img/army_icons1.jpg" width='30px'><br>
            <input type='checkbox' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <img src="assets/img/army_icons2.jpg" width='30px'><br>
            <input type='checkbox' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <img src="assets/img/army_icons3.jpg" width='30px'><br>
            <input type='checkbox' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <img src="assets/img/army_icons4.jpg" width='30px'><br>
            <input type='checkbox' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <img src="assets/img/army_icons5.jpg" style="margin-top: -8px" width='30px'><br>
            <input type='checkbox' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <img src="assets/img/army_icons6.jpg" width='30px'><br>
            <input type='checkbox' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <img src="assets/img/army_icons7.jpg" width='30px'><br>
            <input type='checkbox' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <img src="assets/img/army_icons8.jpg" width='30px'><br>
            <input type='checkbox' >
          </fieldset>
        </div>
        <div class='col-sm-1'>
          <fieldset>
            <label for=''>Status</label><br>
            <select name='' ref='status'>
              <option value='Y'>Y</option>
              <option value='N'>N</option>
            </select>
          </fieldset>
        </div>
      </div>
      <div class='row'>
        <div class='col-sm-4'>
          <fieldset>
            <label for=''>Field A</label><br>
            <input ref='fieldA' type='input' >
          </fieldset>
        </div>
        <div class='col-sm-4'>
          <fieldset>
            <label  for=''>Field B</label><br>
            <input ref='fieldB' type='input' >
          </fieldset>
        </div>
        <div class='col-sm-4'>
          <fieldset>
            <label for=''>Field C</label><br>
            <input ref='fieldC' type='input'>
          </fieldset>
        </div>
      </div>
      <div class='row'>
        <div class='col-sm-12'>
          <label for='' scope='col' style='float: left; margin-left: 20px;'>Description</label><br>
          <textarea rows='3' ref='description' style='width: 98%;'></textarea>
        </div>
      </div>
      <div class='row tree-control-actions'>
          <div class='col-lg-6 tree-action-left'>
            <button class='btn btn-secondary' @click='insertBelow'>Insert Below</button>
            <button class='btn btn-secondary' @click='insertChild'>Insert Child</button>
          </div>
          <div class='col-lg-6 tree-action-right'>
            <button class='btn btn-secondary' @click='cancel'>Cancel</button>
            <button class='btn btn-secondary' @click='storeAllXmlData'>Apply</button>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import Tree from './Tree.vue'
import axios from 'axios'
import xml2js from 'xml2js'
import json2xml from 'json2xml'
import eventBus from '../../event-bus'
import { allTreeDatas, itemCount } from '../../util/glovalbars.js'

console.log(itemCount)
console.log(allTreeDatas)
export default {
  name: 'TreeControl',
  components: {
    Tree
  },
  data: function () {
    return {
      search: null,
      value: '',
      treeDisplayData: [
        {
          sortCord: '12',
          description: 'root 1',
          id: 1,
          checkable: true,
          nodes: [
            {
              sortCord: '12',
              description: 'Child 1',
              state: { checked: true },
              id: 3,
              nodes: [
                {
                  sortCord: '12',
                  description: 'Grandchild 1',
                  id: 15
                },
                {
                  sortCord: '12',
                  description: 'Grandchild 2',
                  id: 6
                }
              ]
            },
            {
              sortCord: '12',
              description: 'Child 2',
              id: 4
            }
          ]
        },
        {
          sortCord: '12',
          description: 'Root 2',
          id: 2
        }
      ]
    }
  },
  computed: {
    myCustomStyles () {
      return {
        tree: {
          height: 'auto',
          maxHeight: '300px',
          overflowY: 'visible',
          display: 'inline-block',
          textAlign: 'left'
        },
        row: {
          style: {
            width: '500px',
            cursor: 'pointer'
          },
          child: {
            class: '',
            style: {
              height: '35px'
            },
            active: {
              style: {
                height: '35px'
              }
            }
          }
        },
        rowIndent: {
          paddingLeft: '20px'
        },
        text: {
          // class: '' // uncomment this line to overwrite the 'capitalize' class, or add a custom class
          style: {},
          active: {
            style: {
              'font-weight': 'bold',
              color: '#2ECC71'
            }
          }
        }
      }
    },
    myCustomOptions () {
      return {
        treeEvents: {
          expanded: {
            state: false
          },
          collapsed: {
            state: false
          },
          selected: {
            state: true,
            fn: this.mySelectedFunction
          },
          checked: {
            state: true,
            fn: this.myCheckedFunction
          }
        },
        events: {
          expanded: {
            state: true
          },
          selected: {
            state: true
          },
          checked: {
            state: true
          },
          editableName: {
            state: true,
            fn: null,
            calledEvent: 'selected'
          }
        },
        addNode: {
          state: false,
          fn: this.addNodeFunction,
          appearOnHover: false
        },
        editNode: {
          state: false,
          fn: null,
          appearOnHover: false
        },
        deleteNode: {
          state: true,
          fn: this.deleteNodeFunction,
          appearOnHover: true
        },
        showTags: true
      }
    }
  },
  mounted () {
    eventBus.$on('treePr', () => {
      this.treePr()
    })
    eventBus.$on('treeGr', () => {
      this.treeGr()
    })
    eventBus.$on('treeRs', () => {
      this.treeRs()
    })
    eventBus.$on('treeDp', () => {
      this.treeDp()
    })
    eventBus.$on('treeTe', () => {
      this.treeTe()
    })
    eventBus.$on('treeDi', () => {
      this.treeDi()
    })
    eventBus.$on('treeDr', () => {
      this.treeDr()
    })
    eventBus.$on('treeTr', () => {
      this.treeTr()
    })
    eventBus.$on('treeAt', () => {
      this.treeAt()
    })
    eventBus.$on('treeVt', () => {
      this.treeVt()
    })
    eventBus.$on('treeAl', () => {
      this.treeAl()
    })
    eventBus.$on('treeBl', () => {
      this.treeBl()
    })
    eventBus.$on('treeIi', () => {
      this.treeIi()
    })
  },

  methods: {
    myCheckedFunction: function (nodeId, state) {
      console.log(`is ${nodeId} checked ? ${state}`)
      console.log(this.$refs['my-tree'].getCheckedNodes('id'))
      console.log(this.$refs['my-tree'].getCheckedNodes('description'))
    },
    mySelectedFunction: function (nodeId, state) {
      console.log(`is ${nodeId} selected ? ${state}`)
      const node = this.$refs['my-tree'].findNode(nodeId)
      const newState = node.state
      newState.checked = state
      this.$set(node, 'state', newState)
    },
    deleteNodeFunction: function (node) {
      const nodePath = this.$refs['my-tree'].findNodePath(node.id)
      const parentNodeId = nodePath.slice(-2, -1)[0]
      if (parentNodeId === undefined) {
        // 'root' node
        console.log('deleteParent', parentNodeId)
        const nodeIndex = this.$refs['my-tree'].nodes.findIndex((x) => x.id !== node.id) - 1
        this.$refs['my-tree'].nodes.splice(nodeIndex, 1)
        // this.allTreeDatas.splice(nodeIndex, 1)
      } else {
        // child node
        const parentNode = this.$refs['my-tree'].findNode(parentNodeId)
        const nodeIndex = parentNode.nodes.findIndex((x) => x.id !== node.id) - 1
        parentNode.nodes.splice(nodeIndex, 1)
      }
      console.log('example: remove node', node.id)
    },
    addNodeFunction: function (newChild) {
      var selectedNode = this.$refs['my-tree'].getSelectedNode()
      if (selectedNode.nodes === undefined || selectedNode.nodes.length === 0) {
        // the node doesn't have childs
        // I use $set to ensure that VueJs detect the change
        this.$set(selectedNode, 'nodes', [newChild])
      } else {
        selectedNode.nodes.push(newChild)
      }
    },
    // Actions for Tree
    insertBelow: function () {
      var selectedNode = this.$refs['my-tree'].getSelectedNode()
      const nodePath = this.$refs['my-tree'].findNodePath(selectedNode.id)
      const parentNodeId = nodePath.slice(-2, -1)[0]
      var newNode = this.getInputedData(true)
      if (newNode === false) return
      this.allTreeDatas.push(newNode)
      if (parentNodeId === undefined) {
        // 'root' node
        const nodeIndex = this.$refs['my-tree'].nodes.findIndex((x) => x.id === selectedNode.id) + 1
        this.$refs['my-tree'].nodes.splice(nodeIndex, 0, newNode)
      } else {
        // child node
        const parentNode = this.$refs['my-tree'].findNode(parentNodeId)
        const nodeIndex = parentNode.nodes.findIndex((x) => x.id === selectedNode.id) + 1
        parentNode.nodes.splice(nodeIndex, 0, newNode)
      }
    },
    insertChild: function () {
      var newChild = this.getInputedData(false)
      if (newChild === false) {
        return
      }
      this.allTreeDatas.push(newChild)
      this.addNodeFunction(newChild)
    },
    storeAllXmlData: function () {
      var FileSaver = require('file-saver')
      var jsonArray = []
      this.allTreeDatas.forEach(obj => {
        var jsonData = { treete_element: '' }
        jsonData.treete_element = obj
        jsonArray.push(jsonData)
      })
      var dd = { DD: jsonArray }
      var convertedXml = json2xml(dd)
      var blob = new Blob([convertedXml], { type: 'xml/plain;charset=utf-8' })
      FileSaver.saveAs(blob, 'hello.xml')
    },
    cancel: function () {
      window.alert('cancel clicked!')
    },
    // generating functions new data and id
    getLastId: function (maxId) {
      let len = 4 - maxId.toString().length
      if (len == 0) {
        return maxId.toString()
      } else if (len == 1) {
        return '.0' + maxId.toString()
      } else if (len == 2) {
        return '.00' + maxId.toString()
      } else if (len == 3) {
        return '.000' + maxId.toString()
      }
    },
    generateChildId: function (node) {
      var idArray = []
      this.allTreeDatas.forEach(item => {
        if (item.parent_id.trim() === node.id.trim()) {
          let splitedId = item.id.trim().split('.')
          let len = splitedId.length
          let lastId = splitedId[len - 1]
          if (parseInt(lastId) === 9999) {
            window.alert('You can not add the node because Id is 9999')
            return false
          }
          idArray.push(parseInt(lastId))
        }
      })
      let maxId = Math.max.apply(null, idArray) + 1
      if (idArray.length === 0) maxId = 0
      let lastId = this.getLastId(maxId)
      return node.id.concat(lastId).trim()
    },
    generateFriendId: function (node) {
      var idArray = []
      this.allTreeDatas.forEach(item => {
        if (item.parent_id.trim() === node.parent_id.trim()) {
          let splitedId = item.id.trim().split('.')
          let len = splitedId.length
          let lastId = splitedId[len - 1]
          if (parseInt(lastId) === 9999) {
            window.alert('You can not add the node because Id is 9999')
            return false
          }
          idArray.push(parseInt(lastId))
        }
      })
      let maxId = Math.max.apply(null, idArray) + 1
      let lastId = this.getLastId(maxId)
      if (node.parent_id === 0 || node.parent_id === '') {
        return lastId.slice(1).trim()
      } else {
        return node.parent_id.concat(lastId).trim()
      }
    },
    getInputedData: function (flag) {
      var selectedNode = this.$refs['my-tree'].getSelectedNode()
      let id = flag == true ? this.generateFriendId(selectedNode) : this.generateChildId(selectedNode)
      if (id === false) return false
      let pId = flag == true ? selectedNode.parent_id.trim() : selectedNode.id.trim()
      let currentDate = new Date()
      let date = ('0' + currentDate.getDate()).slice(-2)
      let month = ('0' + (currentDate.getMonth() + 1)).slice(-2)
      let year = currentDate.getFullYear()
      let hours = currentDate.getHours()
      let minutes = currentDate.getMinutes()
      let seconds = currentDate.getSeconds()
      let updateDate = year + '-' + month + '-' + date + ' ' + hours + ':' + minutes + ':' + seconds
      var rowItem = {
        id: `${id}`,
        parent_id: `${pId}`,
        iconType: 'knif.jpg',
        sortCord: this.$refs['sort-cord'].value,
        status: this.$refs['status'].value,
        fieldA: this.$refs['fieldA'].value,
        fieldB: this.$refs['fieldB'].value,
        fieldC: this.$refs['fieldC'].value,
        flags: 'flag1',
        lastUpdate: updateDate,
        description: this.$refs['description'].value,
        nodes: []
      }
      return rowItem
    },
    // Londing functions for coming from xml
    findAllChild: function (parentItem) {
      this.allTreeDatas.forEach(item => {
        if (item.parent_id.trim() === parentItem.id.trim()) {
          parentItem.nodes.push(item)
          this.itemCount--
        }
      })
      if (parentItem.nodes.length == 0) return
      parentItem.nodes.forEach(node => {
        this.findAllChild(node)
      })
      if (this.itemCount == 0) return parentItem
    },
    findLevelItems: function (len) {
      let levelItems = []
      this.allTreeDatas.forEach(item => {
        if (item.id.split('.').length === len) {
          levelItems.push(item)
        }
      })
      return levelItems
    },
    setChildItemsCount: function (startItem) {
      this.allTreeDatas.forEach(item => {
        if (item.id.split('.')[0] == startItem.id && startItem.id.split('.').length !== item.id.split('.').length) {
          this.itemCount += 1
        }
      })
    },
    convertTreeData: function () {
      let rootItems = this.findLevelItems(1)
      let convertedData = []
      rootItems.forEach(rootItem => {
        this.itemCount = 0
        this.setChildItemsCount(rootItem)
        this.itemCount == 0 ? convertedData.push(rootItem) : convertedData.push(this.findAllChild(rootItem))
      })
      return convertedData
    },
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
    // Tree actions relavant to tree type
    treeTe: function () {
      var ref = this
      axios.get('assets/hello.xml').then(async (response) => {
        let treeData = await this.parseXML(response.data)
        var treeElements = treeData.DD.treete_element
        treeElements.forEach(element => {
          element.nodes = []
        })
        this.allTreeDatas = treeElements
        var structedTreeData = this.convertTreeData()
        ref.treeDisplayData = structedTreeData
      })
    },
    searchFunc: function (value) {
      this.search = value
      var filteredData = this.customData.filter(node => node.text.includes(value))
      this.treeDisplayData = filteredData
    }
  },
  beforeDestroy () {
    eventBus.$off('storeXmlData')
  }
}

</script>

<style>
  #hole-tree {
    border: solid gray 2px;
    width: 94%;
    margin-left: 1%;
    height: 260px;
  }
  #tree-body-header button{
    color: gray;
    width: 100%;
    margin: 5px;
    text-align: center;
    color: white;
  }
  #tree-body-header {
    /* height: 19%;
    max-height: 50px; */
  }
  #tree-body-body {
    /* height: 81%;
    max-height: 210px;
    margin-top: 10px;
    padding-left: 0px; */
  }
  /* tree--control */
  #tree-control {
    /* margin-top: 10px; */
  }
  .tree-control-actions button{
    width: 15%;
    margin: 5px;
    color: white;
  }
  .tree-action-left button{
    margin-left: 50px;
    float: left;
    width: 200px;
  }
  .tree-action-right button{
    /* margin-right: 50px; */
    width: 100px;
    float: right;
  }
</style>
