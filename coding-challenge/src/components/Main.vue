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

      totalItems.forEach(item => {


        if (item.local_quantity > 0 && this.taxExcemptions.includes(item.type) && item.price > 0) {
          //On Books, Food and Medical items there is no sales tax. So we will just add price in existing total.
          this.itemsSalesTax.push({ "title": item.title, "salesTax": 0, "priceInclAllTaxes": (parseFloat(item.price)).toFixed(2) })
          this.total = parseFloat(this.total) + parseFloat(item.price)
          this.total = this.total.toFixed(2)
        }

        if (item.local_quantity > 0 && !this.taxExcemptions.includes(item.type) && item.price > 0) {
          //Adding sales tax on non-imported & non-excempted items. 
          let salesTax = this.percentageCalculator(this.basicSalesTaxPercnt, parseFloat(item.price))
          let priceInclTax = parseFloat(item.price) + parseFloat(salesTax);
          priceInclTax = priceInclTax.toFixed(2)
          this.itemsSalesTax.push({ "title": item.title, "salesTax": (parseFloat(salesTax)).toFixed(2), "priceInclAllTaxes": priceInclTax })
          this.total = parseFloat(this.total) + (parseFloat(item.price) + parseFloat(salesTax))
          this.total = this.total.toFixed(2)
          this.totalSalesTax = this.totalSalesTax + salesTax
        }
        //Adding imported tax on imported items
        if (item.imported_quantity !== 0 && this.importedPrice !== 0) {
          let importTax = this.percentageCalculator(this.importedTaxPercnt, parseFloat(item.importedPrice))
          let salesTax = 0.00;
          let priceInclTax = 0.00;
          if (this.taxExcemptions.includes(item.type)) {
            priceInclTax = parseFloat(item.importedPrice) + parseFloat(importTax);
            priceInclTax = priceInclTax
            this.itemsSalesTax.push({ "title": item.title, "salesTax": (parseFloat(salesTax)), "priceInclAllTaxes": priceInclTax })
            this.total = parseFloat(this.total) + (parseFloat(item.importedPrice) + parseFloat(importTax))
            this.total = this.total.toFixed(2)
            this.totalSalesTax = this.totalSalesTax + salesTax.toFixed(2);
          }
          else {
            salesTax = this.percentageCalculator(this.basicSalesTaxPercnt, parseFloat(item.importedPrice))
            priceInclTax = parseFloat(item.importedPrice) + parseFloat(importTax) + parseFloat(salesTax);
            priceInclTax = priceInclTax
            this.itemsSalesTax.push({ "title": item.title, "salesTax": (parseFloat(salesTax)), "priceInclAllTaxes": priceInclTax })
            this.total = parseFloat(this.total) + (parseFloat(item.importedPrice) + parseFloat(importTax) + parseFloat(salesTax))
            this.total = this.total.toFixed(2)
            this.totalSalesTax = this.totalSalesTax + salesTax.toFixed(2);
          }
          

        }
      });

    },
    percentageCalculator(percent, price) {
      //Function to return percentage of a number with a rounded off figure with 2 decimals.
      let result = parseFloat((percent / 100) * price);   //for example: Number = 0.565
      console.log(result)
      let factor = (result + "").split(".")[1];             // number = 565
      let first_decimalNumber = factor[0]                 // 5
      let second_decimalNumber = factor[1]                // 6
      if (second_decimalNumber > 5 && second_decimalNumber > 0) {
        let newFactor = (parseInt(first_decimalNumber) + 1).toString() + '0'
        let roundedDecimals = newFactor[0] + newFactor[1];
        result = (result + "").split(".")[0];
        result = result + "." + roundedDecimals;   
      }

      else if (second_decimalNumber < 5 && second_decimalNumber > 0) {
        let newFactor = second_decimalNumber + 0
        let roundedDecimals = newFactor[0] + newFactor[1];
        result = (result + "").split(".")[0];
        result = result + "." + roundedDecimals;
      }
     
      return result;
    },

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
