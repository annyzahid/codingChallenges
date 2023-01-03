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
    <!-- Input Container for Books -->
    <v-container class="grey lighten-2" style="height: 11rem;width: 70%">
      <v-row class="mb-6" no-gutters>
        <v-col md="2">
          <h2 style="margin-top: 3rem">Book</h2>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="4">
              <v-text-field v-model="book.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model="book.imported_quantity" label="Imported" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model="book.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model="book.importedPrice" :rules="priceRules" label="€"></v-text-field>
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
              <v-text-field v-model="musicCd.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model="musicCd.imported_quantity" label="Imported" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model="musicCd.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model="musicCd.importedPrice" :rules="priceRules" label="€"></v-text-field>
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
              <v-text-field v-model="chocolate.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model="chocolate.imported_quantity" label="Imported" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model="chocolate.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model="chocolate.importedPrice" :rules="priceRules" label="€"></v-text-field>
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
              <v-text-field v-model="perfume.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model="perfume.imported_quantity" label="Imported" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model="perfume.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model="perfume.importedPrice" :rules="priceRules" label="€"></v-text-field>
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
              <v-text-field v-model="headachePills.local_quantity" label="Local" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-text-field v-model="headachePills.imported_quantity" label="Imported" :rules="priceRules" outlined :min="0"
                type="number" clearable></v-text-field>
            </v-col>
          </v-row>
        </v-col>
        <v-col md="4">
          <v-row class="mb-6" no-gutters>
            <v-col md="3">
              <v-text-field v-model="headachePills.price" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="3">
              <v-text-field v-model="headachePills.importedPrice" :rules="priceRules" label="€"></v-text-field>
            </v-col>
          </v-row>
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
        price: "",
        importedPrice: "",
        imported: false,
        imported_quantity: 0,
        local: false,
        local_quantity: 0,
      },
      musicCd: {
        price: "",
        importedPrice: "",
        imported: false,
        imported_quantity: 0,
        local: false,
        local_quantity: 0,
      },
      chocolate: {
        price: "",
        importedPrice: "",
        imported: false,
        imported_quantity: 0,
        local: false,
        local_quantity: 0,
      },
      chocolate: {
        price: "",
        importedPrice: "",
        imported: false,
        imported_quantity: 0,
        local: false,
        local_quantity: 0,
      },
      perfume: {
        price: "",
        importedPrice: "",
        imported: false,
        imported_quantity: 0,
        local: false,
        local_quantity: 0,
      },

      headachePills: {
        price: "",
        importedPrice: "",
        imported: false,
        imported_quantity: 0,
        local: false,
        local_quantity: 0,
      },
      checkbox: true,
    };
  },
  methods:{
    
  }
};
</script>
<style lang="scss">
.v-input__icon--clear {
  display: none;
}
</style>
