<template>
  <h1>Client Storage</h1>
</template>
<script>
export default {
  mounted() {
    let openRequest = indexedDB.open("users", 1);
    // user adalah nama database dan 1 adalah versinya

    openRequest.onupgradeneeded = function () {
      // dijalankan bila client tidak memiliki database
      // ...menjalankan inisialisasi...
      let db = openRequest.result;
      // melanjutkan untuk bekerja dengan database menggunakan db object
      console.log("sukses");

      // jika tidak ada "users" store yang diinisialisasi, akan membuat satu
      if (!db.objectStoreNames.contains("users")) {
        let objectStore = db.createObjectStore("users", {
          keyPath: "id",
          autoIncrement: true,
        });
      }

      // buka transaction read/write
      let transaction = db.transaction("users", "readwrite");
      // mendapatkan object store yang kita ingin operasikan
      let userStore = transaction.objectStore("users");
      // menambahkan data pada store
      userStore.add({
        first: "Victoria",
        last: "Lo",
      });
      // menyelesaikan transaksi
      transaction.oncomplete = function () {
        console.log("Transaction is complete");
      };

      // Read
      userStore.get("Victoria");
      // Read
      console.log("indexdb", userStore.get("Victoria"));
    };
    openRequest.onerror = function () {
      console.error("Error", openRequest.error);
    };
    openRequest.onsuccess = function () {};

    // Create;
    const user = { first: "Victoria", last: "AAA" };
    // seperti menyimpan stringified JSON
    localStorage.setItem("user-me", JSON.stringify(user));

    // Read
    console.log("localstirage", JSON.parse(localStorage.getItem("user")));
    //output akan menjadi JSON: {first: "Victoria", last: "lo"}

    // Update
    const update = { first: "Victoria edit", last: "Lo edit" };
    localStorage.setItem("user", JSON.stringify(update));

    // // Delete
    // localStorage.removeItem("user");

    // Create;
    // seperti menyimpan stringified JSON
    sessionStorage.setItem("user-me", JSON.stringify(user));

    // Read
    console.log("localstirage", JSON.parse(sessionStorage.getItem("user")));
    //output akan menjadi JSON: {first: "Victoria", last: "lo"}

    // Update
    sessionStorage.setItem("user", JSON.stringify(update));

    // Delete
    sessionStorage.removeItem("user");

    if (typeof window !== "undefined") {
      console.log("You are on the browser");
      // 👉️ can use localStorage here
    } else {
      console.log("You are on the server");
      // 👉️ can't use localStorage
    }

    // Create;
    document.cookie = "name=victoria edit";

    //Read
    console.log("cookie", document.cookie);

    //Update
    document.cookie = "name=victoria lo";

    //Delete - Menetapkan tanggal kadaluwarsa yang telah berlalu
    document.cookie =
      "name=victoria lo ; expires = Mon, 25 Apr 2022 00:00:00 GMT";
  },
};
</script>
