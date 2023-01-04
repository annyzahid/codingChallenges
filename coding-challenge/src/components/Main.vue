<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">Coding Challenge</h1>

        <p class="subheading font-weight-regular">
          Basic sales tax is applicable at a rate of 10% on all goods, except
          books, food, and medical products that are exempt. Import duty is an
          additional sales tax applicable on all imported goods at a rate of 5%,
          with no exemptions. When I purchase items I receive a receipt which
          lists the name of all the items and their price (including tax),
          finishing with the total cost of the items, and the total amounts of
          sales taxes paid. The rounding rules for sales tax are that for a tax
          rate of n%, a shelf price of p contains (np/100 rounded up to the
          nearest 0.05) amount of sales tax.
        </p>
      </v-col>
    </v-row>
    <v-container>
      <div class="text-center">
        <v-btn tile color="error" @click="clearAll()">
          <v-icon left>
            mdi-cancel
          </v-icon>
          Clear All
        </v-btn>
        <v-btn tile color="success" @click="salesTaxCalculation()" style="margin-left: 1rem;">
          <v-icon left>
            mdi-cart
          </v-icon>
          Checkout
        </v-btn>
      </div>
    </v-container>
    <!-- Input Container for Books -->
    <v-container class="grey lighten-2" style="height: 11rem;width: 70%">
      <v-row class="mb-6" no-gutters>
        <v-col md="2">
          <h2 style="margin-top: 3rem">Book</h2>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="4">
              <v-text-field v-model.lazy="book.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model.lazy="book.imported_quantity" label="Imported" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model.lazy="book.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>

          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model.lazy="book.importedPrice" :rules="priceRules" label="€"></v-text-field>
            </v-col>

          </v-row>
        </v-col>

      </v-row>

    </v-container>

    <!-- Input Container for Music CD -->
    <v-container class="grey lighten-2" style="height: 11rem;margin-top: 1rem;width: 70%">
      <v-row class="mb-6" no-gutters>
        <v-col md="2">
          <h2 style="margin-top: 3rem">Music CD</h2>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="4">
              <v-text-field v-model.lazy="musicCd.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model.lazy="musicCd.imported_quantity" label="Imported" :rules="priceRules" outlined
                :min="0" type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model.lazy="musicCd.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model.lazy="musicCd.importedPrice" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>

    <!-- Input Container for Chocolate -->
    <v-container class="grey lighten-2" style="height: 11rem;margin-top: 1rem;width: 70%">
      <v-row class="mb-6" no-gutters>
        <v-col md="2">
          <h2 style="margin-top: 3rem">Chocolate</h2>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="4">
              <v-text-field v-model.lazy="chocolate.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model.lazy="chocolate.imported_quantity" label="Imported" :rules="priceRules" outlined
                :min="0" type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model.lazy="chocolate.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model.lazy="chocolate.importedPrice" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>

    <!-- Input Container for Chocolate -->
    <v-container class="grey lighten-2" style="height: 11rem;margin-top: 1rem;width: 70%">
      <v-row class="mb-6" no-gutters>
        <v-col md="2">
          <h2 style="margin-top: 3rem">Perfume</h2>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="4">
              <v-text-field v-model.lazy="perfume.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model.lazy="perfume.imported_quantity" label="Imported" :rules="priceRules" outlined
                :min="0" type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model.lazy="perfume.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model.lazy="perfume.importedPrice" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>

    <!-- Input Container for Headache Pills -->
    <v-container class="grey lighten-2" style="height: 11rem;margin-top: 1rem;width: 70%">
      <v-row class="mb-6" no-gutters>
        <v-col md="2">
          <h2 style="margin-top: 3rem">Headache Pills</h2>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="4">
              <v-text-field v-model.lazy="headachePills.local_quantity" label="Local" :rules="priceRules" outlined
                :min="0" type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model.lazy="headachePills.imported_quantity" label="Imported" :rules="priceRules" outlined
                :min="0" type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model.lazy="headachePills.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model.lazy="headachePills.importedPrice" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
    <v-container>
      <div class="text-center">
        <v-btn tile color="error" @click="clearAll()">
          <v-icon left>
            mdi-cancel
          </v-icon>
          Clear All
        </v-btn>
        <v-btn tile color="success" @click="salesTaxCalculation()" style="margin-left: 1rem;">
          <v-icon left>
            mdi-cart
          </v-icon>
          Checkout
        </v-btn>
      </div>
    </v-container>
    <v-container>
      <v-divider style="background-color: black;"></v-divider>
      <v-divider style="background-color: black;"></v-divider>
      <v-divider style="background-color: black;"></v-divider>
    </v-container>
    <v-container class="grey lighten-2" style="height: 11rem;margin-top: 1rem;width: 70%" v-if="itemsSalesTax.length !== 0">
      <v-row class="mb-12" no-gutters>
        <v-col md="2">
          <h2 style="margin-top: 3rem">TOTAL</h2>
        </v-col>
        <v-col md="10">
          <div v-for="(item, index) in itemsSalesTax" :key="index">
            <h3 style="font-size: 1rem;margin-top: 1rem;margin-left: 25rem;">{{ "€" + item.priceInclAllTaxes + " : 1 " + item.title}}</h3>
            <v-divider v-if="index+1 === itemsSalesTax.length" style="background-color: black;"></v-divider>
          </div>
          
          <h3 style="margin-top: 1rem;margin-left: 25rem;">{{ "Sales Tax : " + totalSalesTax }}</h3>
          <h2 style="margin-top: 1rem;margin-left: 25rem;color:red">{{ "Total : " + total }}</h2>
        </v-col>
      </v-row>
    </v-container>

  </v-container>
</template>

<script>
export default {
  name: "Main",
  components: {},
  data() {
    return {
      priceRules: [(v) => v >= 0],
      book: {
        price: 0.00,
        title: 'Book',
        importedPrice: 0.00,
        imported_quantity: 0,
        type: 'books',
        local_quantity: 0,
      },
      musicCd: {
        price: 0.00,
        title: 'Music CD',
        importedPrice: 0.00,
        imported_quantity: 0,
        type: 'entertainment',
        local_quantity: 0,
      },
      chocolate: {
        price: 0.00,
        importedPrice: 0.00,
        title: 'Chocolate',
        imported_quantity: 0,
        type: 'food',
        local_quantity: 0,
      },
      perfume: {
        price: 0.00,
        importedPrice: 0.00,
        title: 'Perfume',
        type: 'cosmetics',
        imported_quantity: 0,
        local_quantity: 0,
      },

      headachePills: {
        price: 0.00,
        importedPrice: 0.00,
        title: 'Headache Pills',
        type: 'medical',
        imported_quantity: 0,
        local_quantity: 0,
      },
      taxExcemptions: ['medical', 'food', 'books'],
      basicSalesTaxPercnt: 10,
      importedTaxPercnt: 5,
      total: 0.00,
      totalSalesTax: 0,
      itemsSalesTax: [],
    };
  },
  methods: {
    salesTaxTotal() {
      let allSalesTaxes = 0;
      if (this.priceInclAllTaxes) {
        this.priceInclAllTaxes.forEach(item => {
          allSalesTaxes = allSalesTaxes + item.salesTax;
        });
      }
      return allSalesTaxes;
    },
    salesTaxCalculation() {
      let totalItems = [];
      totalItems.push(this.book);
      totalItems.push(this.chocolate);
      totalItems.push(this.musicCd);
      totalItems.push(this.perfume);
      totalItems.push(this.headachePills);

      // Note: parseFloat is basically converting/casting string to float value. Why string initally because it's comming from HTML. toFixed(2) is taking 2 digits after decimal.
      totalItems.forEach(item => {

        // First condition is checking whether the added item is in tax-excemptions array & price and quantity is not zero. 
        // First condition is only for non-imported items.
        if (item.local_quantity > 0 && this.taxExcemptions.includes(item.type) && item.price > 0) {
          //On Books, Food and Medical items there is no sales tax. So adding non-imported & sales tax excempted items.

          //Here we have salesTax = 0 in our object because item is from excempted category.
          this.itemsSalesTax.push({ "title": item.title, "salesTax": 0, "priceInclAllTaxes": (parseFloat(item.price)).toFixed(2) })

          // Adding price of item to exisitng total. Initially the total is zero.
          this.total = parseFloat(this.total) + parseFloat(item.price)
          this.total = this.total.toFixed(2)
        }

        // Second condition is also for non-imported item but this time the item is not in tax excemption array.
        if (item.local_quantity > 0 && !this.taxExcemptions.includes(item.type) && item.price > 0) {

          //Adding sales tax on non-imported & non-excempted items. Getting rounded nearest percentage calculation of price.
          // Sales tax percentage and price is passed to funtion.
          let salesTax = this.percentageCalculator(this.basicSalesTaxPercnt, parseFloat(item.price))

          // Here the Tax included price is summed up.
          let priceInclTax = parseFloat(item.price) + parseFloat(salesTax);
          priceInclTax = priceInclTax.toFixed(2)
          
          // Now the object with all the required details is pushed in array of items which has tax calculation too.
          this.itemsSalesTax.push({ "title": item.title, "salesTax": (parseFloat(salesTax)).toFixed(2), "priceInclAllTaxes": priceInclTax })
          this.total = parseFloat(this.total) + (parseFloat(item.price) + parseFloat(salesTax))
          this.total = this.total.toFixed(2)

          // In the first condition there was no sales tax but now there is a sales tax and we will add it to total salesTax collected on current totalSales Tax.
          // Initially the totalSalesTax is zero.
          this.totalSalesTax = this.totalSalesTax + salesTax
        }
        // Third condition is for those items which are imported. Now Sales tax will also apply for this item.
        if (item.imported_quantity !== 0 && this.importedPrice !== 0) {

          //Here we will get the Import Tax percentage on imported item price.
          let importTax = this.percentageCalculator(this.importedTaxPercnt, parseFloat(item.importedPrice))
          let salesTax = 0.00;  // For sales tax excemption the applied sales tax will always be zero.
          let priceInclTax = 0.00;

          // Here there will be 2 conditions extra to check whether the imported item is in the category of sales tax excemption or not.

          // First condition is for checking that imported item is in tax excemption or not.
          if (this.taxExcemptions.includes(item.type)) {

            // Here we are adding only the import tax to imported item price.
            priceInclTax = parseFloat(item.importedPrice) + parseFloat(importTax);
            priceInclTax = priceInclTax

            this.itemsSalesTax.push({ "title": item.title, "salesTax": (parseFloat(salesTax)), "priceInclAllTaxes": priceInclTax })
            this.total = parseFloat(this.total) + (parseFloat(item.importedPrice) + parseFloat(importTax))
            this.total = this.total.toFixed(2)
            this.totalSalesTax = this.totalSalesTax + salesTax.toFixed(2);
          }
          // Second condition is for imported item is not under sales tax excemption.
          else {
            
            //Since we already have the calcualtion of import tax above so now we will add the sales tax on imported item price.
            salesTax = this.percentageCalculator(this.basicSalesTaxPercnt, parseFloat(item.importedPrice))

            // Here the import price is added with import tax and sales tax to get a price including all tax on this item.
            priceInclTax = parseFloat(item.importedPrice) + parseFloat(importTax) + parseFloat(salesTax);
            priceInclTax = priceInclTax
            this.itemsSalesTax.push({ "title": item.title, "salesTax": (parseFloat(salesTax)), "priceInclAllTaxes": priceInclTax })

            // Here we are adding previous total and  imported price with sales tax and import tax.
            this.total = parseFloat(this.total) + (parseFloat(item.importedPrice) + parseFloat(importTax) + parseFloat(salesTax))
            this.total = this.total.toFixed(2)
            this.totalSalesTax = this.totalSalesTax + salesTax.toFixed(2);
          }
        }
      });

    },
    // This fuction is used to get sales tax on price and import tax on price whenever required.
    percentageCalculator(percent, price) {
      //First we will use simple maths to calculate percentage of a number (price).
      let result = parseFloat((percent / 100) * price);   //for example: Number = 0.56532

      // We split the digits after decimal.
      let factor = (result + "").split(".")[1];             // number = 565
      
      // Here we take first decimal digit.
      let first_decimalNumber = factor[0]                 // number = 5
      
      // Here we take second decimal digit.
      let second_decimalNumber = factor[1]                // number = 6

      // First condition is checking whether second digit is greated than 0 & 5.
      if (second_decimalNumber > 5 && second_decimalNumber > 0) {

        //Rounding off the first decimal digit based on second decimal digit.  For Example => .68 => .70
        let newFactor = (parseInt(first_decimalNumber) + 1).toString() + '0'

        // Now the new after decimal digitals are joined. For Example '7' + '0'  as a string (not as a number)
        let roundedDecimals = newFactor[0] + newFactor[1];  
        
        // Now we remove the after decimal part from orignal result. For Example: '0.68' => '0'
        result = (result + "").split(".")[0];

        // We add the rounded of decimals with the result as a string. For Example: '0' +  '.' + '70' = 0.70
        result = result + "." + roundedDecimals;   
      }

      // Second condition checks if second decimal is less and 5 and greated than 0
      else if (second_decimalNumber < 5 && second_decimalNumber > 0) {

        // Here we just round off the second digit to neared zero. For Example: .64 => .60
        let newFactor = second_decimalNumber + 0

        // Here the first and second(modified) digits are added togther as a string.
        let roundedDecimals = newFactor[0] + newFactor[1];
        result = (result + "").split(".")[0];
        result = result + "." + roundedDecimals;
      }

      // There will be a third condition also 
      /*if(first_decimalNumber === 9 && second_decimalNumber > 5)
      {
        result = (result + "").split(".")[0];  // For Example: 1.98 => 1
        result = result + 1                    //                   => 1+1=2 
        result = result + '.00'                //                   => 2.00
      }*/
     
      return result;
    },

    // This Function is to reset all values to its orignal state. It's totally vue.js trick.
    clearAll() {
      Object.assign(this.$data, this.$options.data?.call(this));
    }
  },
};
</script>
<style lang="scss">
.v-input__icon--clear {
  display: none;
}
</style>
