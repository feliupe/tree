<template>
<div>
  oho
  <tree :data='treeData' ></tree>

</div>
</template>

<script>
// import  { Tree } from "tree-component/vue";
import "tree-component/vue"
import SystemInformation from './LandingPage/SystemInformation'
// type TreeData<T = any> = {
//     text?: string;
//     value?: T; // anything attached to the node
//     icon?: string | false; // the icon class string, or no icon if is false
//     state: TreeNodeState;
//     children?: TreeData<T>[];
//     contextmenu?: string | Function; // the contextmenu component, props: (data: ContextMenuData<T>)
//     component?: string | Function; // the node component, props: (data: TreeData<T>)
// };
 
// type TreeNodeState = {
//     opened: boolean; // whether the node show its children
//     selected: boolean;
//     disabled: boolean; // disabled node can not be selected and deselected
//     loading: boolean; // show the loading icon, usually used when loading child nodes
//     highlighted: boolean;
//     openable: boolean; // can open or close even no children
//     dropPosition: DropPosition;
//     dropAllowed: boolean; // whether the drop action is allowed
// };
 
// enum DropPosition {
//     empty,
//     up,
//     inside,
//     down,
// }

const state = {
    opened: false, // whether the node show its children
    // selected: booleanm,
    // disabled: booleanm, // disabled node can not be selected and deselected
    // loading: booleanm, // show the loading icon, usually used when loading child nodes
    // highlighted: booleanm,
    openable: true, // can open or close even no children
    // dropPosition: DropPositionm,
    // dropAllowed: boolean, // whether the drop action is allowed
}

const data = [
  {id: 'A', parentId: '#', text: 'A', value: 'AA', state},
  {id: 'B', parentId: '#', text: 'B', value: 'bA', state},
  {id: 'C', parentId: 'B', text: 'C', value: 'CA', state},
  {id: 'D', parentId: 'B', text: 'D', value: 'DA', state},
  {id: 'E', parentId: 'A', text: 'E', value: 'EA', state}
]

const tree = {id: '#'}
var parent = {}
var index = {'#': tree}
var needReplace = {}
for (var d of data) {

  index[d.id] = d

  if (needReplace[d.id]) {
    Object.assign(needReplace[d.id], d)
    d = needReplace[d.id]
    delete needReplace(d.id)
  }

  if (index[d.parentId]) {
    parent = index[d.parentId]
  } else {
    parent = {id: d.parentId}
    needReplace[d.parentId] = parent
  }
  parent.children = parent.children || []
  parent.children.push(d)
}

console.log('treee', tree.children.length)

export default {

  data() {
    return {
      treeData: tree.children
    }
  },
  name: 'landing-page',
  // components: { Tree },
  methods: {
    open (link) {
      this.$electron.shell.openExternal(link)
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body { font-family: 'Source Sans Pro', sans-serif; }

  #wrapper {
    background:
      radial-gradient(
        ellipse at top left,
        rgba(255, 255, 255, 1) 40%,
        rgba(229, 229, 229, .9) 100%
      );
    height: 100vh;
    padding: 60px 80px;
    width: 100vw;
  }

  #logo {
    height: auto;
    margin-bottom: 20px;
    width: 420px;
  }

  main {
    display: flex;
    justify-content: space-between;
  }

  main > div { flex-basis: 50%; }

  .left-side {
    display: flex;
    flex-direction: column;
  }

  .welcome {
    color: #555;
    font-size: 23px;
    margin-bottom: 10px;
  }

  .title {
    color: #2c3e50;
    font-size: 20px;
    font-weight: bold;
    margin-bottom: 6px;
  }

  .title.alt {
    font-size: 18px;
    margin-bottom: 10px;
  }

  .doc p {
    color: black;
    margin-bottom: 10px;
  }

  .doc button {
    font-size: .8em;
    cursor: pointer;
    outline: none;
    padding: 0.75em 2em;
    border-radius: 2em;
    display: inline-block;
    color: #fff;
    background-color: #4fc08d;
    transition: all 0.15s ease;
    box-sizing: border-box;
    border: 1px solid #4fc08d;
  }

  .doc button.alt {
    color: #42b983;
    background-color: transparent;
  }
</style>
