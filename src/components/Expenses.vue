<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-6 mt-5" style="height : 10vh">
        <div class="holder">
          <form @submit.prevent>
            <select v-model="category">
              <option
                :name="category.name"
                v-for="category in categories"
                :value="category.name"
                :key="category.id"
              >{{category.name}}</option>
            </select>
            
            <select v-model="time">
              <option
                :name="time.when"
                :value="time.when"
                v-for="time in times"
                :key="time.id"
              >{{time.when}}</option>
            </select>
            
            <input
              v-model.number="price"
              placeholder="Unit Price"
              class="price p-2"
              type="number"
              name="price"
            >
            
            <input
              v-model="expense"
              placeholder="Expense Description"
              class="p-2 mt-2"
              type="text"
              name="description"
            >
            
            <button @click="addExpense" class="mt-2 mb-2 rounded-0 btn btn-large btn-success">SUBMIT</button>
          </form>

          <button @click="print" class="mt-2 mb-2 rounded-0 btn btn-large btn-success">Print</button>
          <transition-group
            tag="ul"
            name="list"
            enter-active-class="animated bounceInUp"
            leave-active-class="animated bounceOutDown"
          >
            <li v-for="(expense, index) in expenses" :key="expense">
              {{expense.title}} {{expense.price}}
              <i
                class="fa fa-minus-circle"
                v-on:click="remove(index)"
              ></i>
            </li>
          </transition-group>

          <p>Kindly input the expenses for the week</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Expenses",
  data() {
    return {
      expense: "", // Add this line
      category: "Feeding",
      time: "Morning",
      price: "",
      id: "",
      categories: [
        { name: "Feeding" },
        { name: "Transportation" },
        { name: "Mobilization" },
        { name: "Miscellaneous" }
      ],

      times: [
        { when: "Morning" },
        { when: "Afternoon" },
        { when: "Evening" },
        { when: "Night-Time" }
      ],

      expenses: [
        { title: "Feeding", category: "Feeding", time: "", price: "200" },
        { title: "Transport", category: "Ca_name", time: "", price: "" }
      ],
      feeding: [{ title: String, category: String, time: String, price: 0 }]
    };
  },
  methods: {
    addExpense() {
      if (this.category === "Feeding") {
        this.feeding.push({
          title: this.expense,
          category: this.category,
          time: this.time,
          price: this.price
        });
      }
      this.expenses.push({
        title: this.expense,
        category: this.category,
        time: this.time,
        price: this.price
      });
      this.expense = "";
      this.price = "";
    },
    remove(id) {
      this.expenses.splice(id, 1);
      // console.log('I work');
    },
    print: function() {
      let total = JSON.stringify(this.feeding); 
      // this.feeding.price = this.feeding.price += this.feeding.price;
      console.log(total);
      console.log(this.feeding.price);

      this.feeding.forEach(feed => {
        feed.price += feed.price;
        console.log(feed.price);
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>
