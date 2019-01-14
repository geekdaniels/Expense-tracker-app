<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-6 mt-5" style="height : 10vh">
        <div class="holder">
          <p class="conc"
          v-if="max_expense_sum === feed_total"
          >You spent more on Feeding</p>
          <p class="conc"
          v-if="max_expense_sum === transport_total"
          >You spent more on Transportation</p>
          <p class="conc"
          v-if="max_expense_sum === Miscellaneous_tot"
          >You spent more on Miscellaneous activities</p>
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

          <button @click="print" class="mt-2 mb-2 rounded-0 btn btn-large btn-success">View Report</button>
          <transition-group
            tag="ul"
            name="list"
            enter-active-class="animated bounceInUp"
            leave-active-class="animated bounceOutDown"
          >
            <li v-for="(expense, index) in expenses" :key="expense">
              {{expense.title}} &#8358;{{expense.price}}
              <i
                class="fa fa-minus-circle"
                v-on:click="remove(index)"
              ></i>
            </li>
          </transition-group>

          <p>Kindly input the expenses for the week</p>
          <p v-if="feed_tot > 1">You spent &#8358;{{feed_tot}} on Feeding</p>
          <p v-if="transport_total > 1">You spent &#8358;{{transport_total}} on Transportation</p>
          <p v-if="Miscellaneous_tot > 1">You spent &#8358;{{Miscellaneous_tot}} on Miscellaneous expenses</p>
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
      feed_tot : 0,
      Miscellaneous_tot: 0,
      transport_total : 0,
      max_expense_sum : Number,
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
        { title: "Feeding", category: "Feeding", time: "", price: "200" }
      ],
      feeding: [{ price: 0 }],
      transportation: [{ price: 0 }],
      Miscellaneous: [{ price: 0 }],
      sum_array : []
    };
  },
  methods: {
    addExpense() {
      if (this.category === "Feeding") {
        this.feeding.push({
          price: this.price
        });
      }else if(this.category === "Transportation"){
        this.transportation.push({
          price: this.price
        });
      }else if(this.category === "Miscellaneous"){
        this.Miscellaneous.push({
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
      let total = JSON.stringify(this.expenses); 
      // this.feeding.price = this.feeding.price += this.feeding.price;
      console.log(total);
      console.log(this.feeding.price);


      function sum(items, prop){
        return items.reduce(function (a, b){
          return a + b[prop];
        }, 0);
      }
      let feed = this.feeding;
      this.feed_tot = sum(feed, 'price');
      
      console.log("feed_total :" + this.feed_tot);

      let transport = this.transportation;
      this.transport_total = sum(transport, 'price');
      console.log("transport_total :" + this.transport_total);

      let Miscellaneous = this.Miscellaneous;
      this.Miscellaneous_tot = sum(Miscellaneous, 'price');
      console.log("Miscellaneous_tot :" + this.Miscellaneous_tot);

      this.sum_array.push(this.feed_tot, this.transport_total, this.Miscellaneous_tot);

      let sum_total = JSON.stringify(this.sum_array);
      console.log(sum_total);

      function max_expense(sum_array){
        return Math.max.apply(Math, sum_array);
      }
      console.log(max_expense(this.sum_array));
this.max_expense_sum = max_expense(this.sum_array)
      console.log("sum :" + this.max_expense_sum);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.conc{
  color: red;
}
</style>
