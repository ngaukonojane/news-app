template>
<div class="container">
<h3>{{ title }} </h3>
<form>
  <textarea placeholder="Add new task" v-model=
  "newTask"></textarea>
  <P>{{newTask}}</P>

  <button type="button" v-on:click="addTask">Add task {{tasks.length}} </button>
</form>

<ul>
<li v-for="task in tasks">{{ task }}
  </li>

</ul>
</div>
</template>

<script>
export default {
data: function() {
return {
title: 'To do App',
newTask:'My new task ',
tasks: [

]
}
},
methods: {
  addTask(){
   this.tasks.unshift(this.newTask);
this.newTask = '';

  }
}
}
</script>
