<template>
<div class="hello">
  <div>
    <label>Goal</label>
    <input type="text" id="goal"  v-model="goal"/>
    <button @click="addGoal" :disabled="goal.length === 0" v-if="!isEditing">Add Goal</button>
    <template v-else>
      <button @click="updateGoal" :disabled="goal.length === 0">Update Goal</button>
      <button @click="updateGoal" :disabled="goal.length === 0" >Cancel</button>
    </template>
  </div>
  <div class="checkbox">
    <label value="goal"> Show goal</label>
    <input type="checkbox" value="checkbox" v-model="goalCheckBox">
    
  </div>
</div>
</template>