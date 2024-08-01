<script setup>
  import { ref } from 'vue';

  const products = ref([
    {
      id: 1,
      name: "珍珠奶茶",
      description: "香濃奶茶搭配QQ珍珠",
      price: 50,
      stock: 20
    },
    {
      id: 2,
      name: "冬瓜檸檬",
      description: "清新冬瓜配上新鮮檸檬",
      price: 45,
      stock: 18
    },
    {
      id: 3,
      name: "翡翠檸檬",
      description: "綠茶與檸檬的完美結合",
      price: 55,
      stock: 34
    },
    {
      id: 4,
      name: "四季春茶",
      description: "香醇四季春茶，回甘無比",
      price: 45,
      stock: 10
    },
    {
      id: 5,
      name: "阿薩姆奶茶",
      description: "阿薩姆紅茶搭配香醇鮮奶",
      price: 50,
      stock: 25
    },
    {
      id: 6,
      name: "檸檬冰茶",
      description: "檸檬與冰茶的清新組合",
      price: 45,
      stock: 20
    },
    {
      id: 7,
      name: "芒果綠茶",
      description: "芒果與綠茶的獨特風味",
      price: 55,
      stock: 18
    },
    {
      id: 8,
      name: "抹茶拿鐵",
      description: "抹茶與鮮奶的絕配",
      price: 60,
      stock: 20
    },
  ])

  const tempProduct = ref(null)

  const subStock = (product) => {
    if (product.stock > 0) {
      product.stock--
    }
  }

  const addStock = (product) => {
    product.stock++
  }

  const editProduct = (product) => {
    tempProduct.value = { ...product }
  }

  const confirmEdit = () => {
    const needToModifyProduct = products.value.find((p) => p.id === tempProduct.value.id)
    
    needToModifyProduct.name = tempProduct.value.name
    needToModifyProduct.description = tempProduct.value.description
    needToModifyProduct.price = tempProduct.value.price
    needToModifyProduct.stock = tempProduct.value.stock

    console.log(needToModifyProduct)

    tempProduct.value = null
  }

  const cancel = () => {
    tempProduct.value = null
  }
</script>

<template>
  <div>
    <h1>2024 vue week1</h1>
    <table>
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col">編輯</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.name }}</td>
          <td><small>{{ product.description }}</small></td>
          <td>{{ product.price }}</td>
          <td>
            <button type="button" @click="subStock(product)">-</button>{{ product.stock }}<button type="button" @click="addStock(product)">+</button>
          </td>
          <td>
            <button type="button" @click="editProduct(product)">修改品項</button>
          </td>
        </tr>
      </tbody>
      <br>
      <div v-if="tempProduct">
        <h2>編輯品項</h2>
        <p>品項：<input type="text" name="" id="" v-model="tempProduct.name"></p>
        <p>描述：<input type="text" name="" id="" v-model="tempProduct.description"></p>
        <p>價格：<input type="text" name="" id="" v-model="tempProduct.price"></p>
        <p>庫存：<input type="text" name="" id="" v-model="tempProduct.stock"></p>
        
        <button type="button" @click="confirmEdit">確認修改</button>
        <button type="button" @click="cancel">取消</button>
      </div>
    </table>
  </div>
</template>