<template>
  <table class="table table-bordered">
  	<tbody>
    <tr v-for="row in items">
      <td v-for="v in row">
        	<trycom v-bind:quest=v></trycom>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script>

var Child = {
  props: ['quest'],
  template: `<div >
               <div class="card-header"> {{quest}}</div>
               <div>
               <p>&nbsp</p>
               <p>&nbsp</p>
               <p>&nbsp</p>
               <p>&nbsp</p>
               </div>
             </div>`
}
var data = {}
for (let j = 0; j < 5; j++) {
  console.log(j)
  data[j] = {}
  for (let i = 0; i < 4; i++) {
    console.log(j)
    data[j][i] = genDivWithRemain()
    console.log(data)
  }
}
for (let j = 5; j < 10; j++) {
  console.log(j)
  data[j] = {}
  for (let i = 0; i < 4; i++) {
    console.log(j)
    data[j][i] = genMixedCalc()
    console.log(data)
  }
}

function genDivWithRemain () {
  let y = Math.round(Math.random() * 8) + 2
  let z = Math.round(Math.random() * y) - 1
  if (z === 0) {
    z = 1
  }
  let x = y * (Math.round(Math.random() * 9) + 1) + z
  return x + ' ÷ ' + y + ' = '
}

function genMultiply () {
  let x = Math.round(Math.random() * 8) + 1
  let y = Math.round(Math.random() * 8) + 1
// return x + '×' + y
  return [x, y]
}

function genDivide () {
  let y = Math.round(Math.random() * 8) + 1
  let x = y * (Math.round(Math.random() * 8) + 2)
  // return x + ' ÷ ' + y
  return [x, y]
}

function genMixedCalc () {
  let x, y, r, mix
  if (Math.random() > 0.5) {
    [x, y] = genDivide()
    mix = x + ' ÷ ' + y
    r = x / y
  } else {
    [x, y] = genMultiply()
    mix = x + ' x ' + y
    r = x * y
  }
  let z = Math.round(Math.random() * 98) + 1
  if (Math.random() > 0.5) {
    if (z > r) {
      mix = z + ' - ' + mix
    } else {
      mix = mix + ' - ' + z
    }
  } else {
    mix = z + ' + ' + mix
  }

  return mix + ' = '
}
// console.log(row)
//  [{'x': 1, 'y': 2}, {'x': 1, 'y': 2}, {'x': 1, 'y': 2}, {'x': 1, 'y': 2}]

export default {
  components: {
    'trycom': Child
  },
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      items: data
    }
  }
}
</script>

