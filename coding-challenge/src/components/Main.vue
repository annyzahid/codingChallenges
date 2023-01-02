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
    <v-container class="grey lighten-2">
      <v-row class="mb-6" no-gutters>
        <v-col md="2">
          <h2 style="margin-top: 3rem"> Book </h2>
        </v-col>
        <v-col md="2">
          <h3> Price </h3>
          <h4 style="margin-top: 1.3rem"> {{ book.price }} </h4>
        </v-col>
        <v-col md="4" >
          <v-row class="mb-6" no-gutters>
            <v-col md="4" style="margin-bottom: -4rem">
              <v-container class="px-0" fluid>
                <v-checkbox
                  v-model="book.imported"
                  :label="`Imported`"
                ></v-checkbox>
              </v-container>
            </v-col>
            <v-col md="1" offset-md="4">
              <v-text-field
                v-model="book.imported_quantity"
                hide-details
                :min="0"
                single-line
                type="number"
              />
            </v-col>
          </v-row>
          <v-row class="mb-6" no-gutters style="margin-top: -1rem">
            <v-col md="4">
              <v-checkbox v-model="book.local" :label="`Local`"></v-checkbox>
            </v-col>
            <v-col md="1" offset-md="4">
              <v-text-field
                v-model="book.local_quantity"
                hide-details
                single-line
                :min="0"
                type="number"
              />
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

  data() {
    return {
      book: {
        price:'€12.49',
        imported: false,
        imported_quantity: 0,
        local: false,
        local_quantity: 0,
      },
      checkbox: true,
    };
  },
};
</script>
