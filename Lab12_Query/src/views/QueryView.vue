<script setup>
import { ref, onMounted, watch } from "vue";
import { collection, query, where, getDocs, limit, orderBy, or, serverTimestamp, doc, setDoc, deleteDoc, addDoc, updateDoc , getCountFromServer , getAggregateFromServer , count} from "firebase/firestore";
import db from "../firebase/init.js";
import Documents from "../components/Documents.vue";
import { useRoute } from "vue-router";

const zips = ref([]);
const title = ref("");
const route = useRoute();

async function getQuery() {
  let qryId = route.params.id;
  zips.value = [];
  let qry = null;
  if (qryId == 1) {
    title.value = "Cities with population > 10,000";
    const zipsRef = collection(db, "zips");
    qry = query(zipsRef, where("pop", ">", 10000), limit(10));
  }
  else if (qryId == 2) {
    title.value = " Cities in Flodia (FL)";
    const zipsRef = collection(db, "zips");
    qry = query(zipsRef, where("state", "==", "FL"), limit(10));
  }
  else if (qryId == 3) {
    title.value = "List zips in DC with population > 40,000";
    const zipsRef = collection(db, "zips");
    qry = query(
      zipsRef,
      where("state", "==", "DC"),
      where("pop", ">", 40000),
      limit(10)
    );
  }
  else if (qryId == 4) {
    title.value = "List zips in FL or in DC with population> 60,000";
    const zipsRef = collection(db, "zips");
    qry = query(
      zipsRef,
      where("state", "in", ["FL", "DC"]),
      where("pop", ">", 60000)
    );
  } else if (qryId == 5) {
    title.value = "List zips in DC or cities with population > 100,000.";
    const zipsRef = collection(db, "zips");
    qry = query(
      zipsRef,
      or(
        where("state", "==", "DC"),
        where("pop", ">", 100000)
      ),
      limit(10)
    );
  }

  else if (qryId == 6) {
    title.value = "List zips in DC and sort the data by population.";
    const zipsRef = collection(db, "zips");
    qry = query(
      zipsRef,
      where("state", "==", "DC"),
      orderBy("pop", "desc"),
      limit(10)
    );
  }
  else if (qryId == 7) {
    title.value = "Latitude (x) Between 71 and 73";
    const zipsRef = collection(db, "zips");
    qry = query(
      zipsRef,
      where("loc.x", ">=", 71),
      where("loc.x", "<=", 73),
      limit(10)
    );
  } else if (qryId == 8) {
    const todoRef = doc(db, "todos", "INT305")
    await setDoc(todoRef, {
      title: "Add another Todo",
      completed: false,
      createdAt: serverTimestamp()
    })
    return
  } else if (qryId == 9) {
    const todoCollRef = collection(db, "todos")
    await addDoc(todoCollRef, {
      title: "Add another todo with addDoc",
      completed: false,
      createdAt: serverTimestamp()
    })
    return
  } else if (qryId == 10) {
    title.value = "10. set completed to be TRUE"
    const todoRef = doc(db, "todos", "INT305")
    await updateDoc(todoRef, {
      completed: true
    })
    return
  } else if (qryId == 11) {
    title.value = "11. delete doc"
    const todoRef = doc(db, "todos", "oRTFQYmRSJl7tf0KSZQy")
    await deleteDoc(todoRef)
    return
  } else if (qryId == 12) {
    const todoCollRef = doc(db, "todos")
    const qry = query(todoCollRef , where('completed','==',true))
    // const snapshot = await getCountFromServer(qry)
    const snapshot = await getAggregateFromServer(qry, {
      countTodo: count
    })
    console.log('Count  :'+snapshot.data().countTodo);
  }









  const querySnap = await getDocs(qry);
  querySnap.forEach((doc) => {
    let data = doc.data();
    data.id = doc.id;
    zips.value.push(data);
  });
}

watch(() => route.params.id, getQuery);

onMounted(() => {
  getQuery();
});
</script>
<template>
  <Documents :title="title" :data="zips" />
</template>

<style></style>
