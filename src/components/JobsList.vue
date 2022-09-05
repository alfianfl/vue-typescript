<template>
  <div class="job-list">
    <p>Ordered by {{order}}</p>
    <transition-group name="list" tag="ul">
        <li v-for="job in orderedJobs" :key="job.id">
            <h2>{{ job.title }} in {{ job.location }}</h2>

            <div class="salary">
            <p>{{ job.salary }}</p>
            </div>
            <div class="description">
            <p>
                Lorem, ipsum dolor sit amet consectetur adipisicing elit.
                Voluptatibus tempore dignissimos unde deleniti accusantium delectus,
                aliquam quasi esse, dolores mollitia veritatis ratione ipsum? Iure
                recusandae doloribus obcaecati dolor atque aliquam?
            </p>
            </div>
        </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, computed } from "vue";
import OrderTerm from "@/types/OrderTerm";
import Job from "@/types/Job";

export default defineComponent({
  props: {
    jobs: {
      require: true,
      default: Array,
      type: Array as PropType<Job[]>,
    },
    order: {
        require:true,
        default: String,
        type: String as PropType<OrderTerm>
    }
  },
  setup(props) {
    const orderedJobs = computed(()=>{

        const newProps = [...props.jobs]
        return newProps.sort((a:Job,b:Job) => {
            return a[props.order] > b[props.order] ? 1 : -1
        })
    })

    return {orderedJobs}
  }
});
</script>

<style scoped>
  .job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move {
    transition: all 1s;
  }
</style>
