<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Listado de Cursos
    </p>

    <section class="antialiased bg-gray-100 text-gray-600 px-4">
    <div class="flex flex-col justify-center">
        <!-- Table -->
        <div class="w-full max-w-2xl mx-auto bg-white shadow-lg rounded-sm border border-gray-200 mt-10">
            <header class="px-5 py-4 border-b border-gray-100">
                <h2 class="font-semibold text-gray-800">Cursos</h2>
            </header>
            <div class="p-3">
                <div class="overflow-x-auto">
                    <table class="table-auto w-full">
                        <thead class="text-xs font-semibold uppercase text-gray-400 bg-gray-50">
                            <tr>
                                <th class="p-2 whitespace-nowrap">
                                    <div class="font-semibold text-left">Profesor</div>
                                </th>
                                <th class="p-2 whitespace-nowrap">
                                    <div class="font-semibold text-left">Asignatura</div>
                                </th>
                                <th>
                                  Acciones
                                </th>
                            </tr>
                        </thead>
                        <tbody class="text-sm divide-y divide-gray-100">
                            <tr v-for="course in courses" :key="course.id">
                                <td class="p-2 whitespace-nowrap">
                                    <div class="flex items-center">
                                        <div class="w-10 h-10 flex-shrink-0 mr-2 sm:mr-3"><img class="rounded-full" src="https://avatars.dicebear.com/v2/male/:seed.svg" width="40" height="40" alt="Alex Shatov"></div>
                                        <div class="font-medium text-gray-800">{{ course.teacher_name }}</div>
                                    </div>
                                </td>
                                <td class="p-2 whitespace-nowrap">
                                    <div class="text-left">{{ course.name }}</div>
                                </td>
                                <td>
                                  <button v-on:click="edit(course.id)" type="button" class="px-2 py-2 font-medium tracking-wide text-black capitalize transition duration-300 ease-in-out transform rounded-xl hover:bg-gray-300 focus:outline-none active:scale-95">
                                    <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#000000">
                                        <path d="M0 0h24v24H0V0z" fill="none"></path>
                                        <path d="M5 18.08V19h.92l9.06-9.06-.92-.92z" opacity=".3"></path>
                                        <path d="M20.71 7.04c.39-.39.39-1.02 0-1.41l-2.34-2.34c-.2-.2-.45-.29-.71-.29s-.51.1-.7.29l-1.83 1.83 3.75 3.75 1.83-1.83zM3 17.25V21h3.75L17.81 9.94l-3.75-3.75L3 17.25zM5.92 19H5v-.92l9.06-9.06.92.92L5.92 19z"></path>
                                    </svg>
                                  </button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
    </section>

    <div class="flex bg-gray-100">
   <div class="m-auto">
      <div>
          <div v-if="errors" class="w-full text-sm border border-t-8 rounded text-red-700 border-red-600 bg-red-100 px-3 py-4 mb-4 mt-6" role="alert">
          <div v-for="(v, k) in errors" :key="k">
              <p v-for="error in v" :key="error" class="text-sm">
                  {{ error }}
              </p>
          </div>
      </div>

         {{ this.response_api }}
         <div class="mt-5 bg-white rounded-lg shadow">
            <div class="flex">
               <div class="flex-1 py-5 pl-5 overflow-hidden">
                  <h1 class="inline text-2xl font-semibold leading-none">Crear Asignaturas</h1>
               </div>
            </div>
            <div class="px-5 pb-5">
               <input placeholder="PROFESOR" v-model="course.teacher_name" class=" text-black placeholder-gray-600 w-full px-4 py-2.5 mt-2 text-base   transition duration-500 ease-in-out transform border-transparent rounded-lg bg-gray-200  focus:border-blueGray-500 focus:bg-white dark:focus:bg-gray-800 focus:outline-none focus:shadow-outline focus:ring-2 ring-offset-current ring-offset-2 ring-gray-400">
               <input placeholder="ASIGNATURA" v-model="course.name" class=" text-black placeholder-gray-600 w-full px-4 py-2.5 mt-2 text-base   transition duration-500 ease-in-out transform border-transparent rounded-lg bg-gray-200  focus:border-blueGray-500 focus:bg-white dark:focus:bg-gray-800 focus:outline-none focus:shadow-outline focus:ring-2 ring-offset-current ring-offset-2 ring-gray-400"> 
           </div>
          
          
            <hr class="mt-4">
            <div class="flex flex-row-reverse p-3">
               <div class="flex-initial pl-3">
                  <button type="button" class="flex items-center px-5 py-2.5 font-medium tracking-wide text-white capitalize   bg-black rounded-md hover:bg-gray-800  focus:outline-none focus:bg-gray-900  transition duration-300 transform active:scale-95 ease-in-out">
                     <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#FFFFFF">
                        <path d="M0 0h24v24H0V0z" fill="none"></path>
                        <path d="M5 5v14h14V7.83L16.17 5H5zm7 13c-1.66 0-3-1.34-3-3s1.34-3 3-3 3 1.34 3 3-1.34 3-3 3zm3-8H6V6h9v4z" opacity=".3"></path>
                        <path d="M17 3H5c-1.11 0-2 .9-2 2v14c0 1.1.89 2 2 2h14c1.1 0 2-.9 2-2V7l-4-4zm2 16H5V5h11.17L19 7.83V19zm-7-7c-1.66 0-3 1.34-3 3s1.34 3 3 3 3-1.34 3-3-1.34-3-3-3zM6 6h9v4H6z"></path>
                     </svg>
                     <button type="button" v-on:click="create"><span class="pl-2 mx-1">Save</span></button>
                  </button>
               </div>
               <div class="flex-initial">
                  <button type="button" class="flex items-center px-5 py-2.5 font-medium tracking-wide text-black capitalize rounded-md  hover:bg-red-200 hover:fill-current hover:text-red-600  focus:outline-none  transition duration-300 transform active:scale-95 ease-in-out">
                     <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px">
                        <path d="M0 0h24v24H0V0z" fill="none"></path>
                        <path d="M8 9h8v10H8z" opacity=".3"></path>
                        <path d="M15.5 4l-1-1h-5l-1 1H5v2h14V4zM6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM8 9h8v10H8V9z"></path>
                     </svg>
                     <span class="pl-2 mx-1">Delete</span>
                  </button>
               </div>
            </div>
         </div>
        
      </div>
   </div>
</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      courses: null,
      response_api: null,
      errors: null,
      course: {
        id: null,
        teacher_name: null,
        name: null,
      }
    }
  },
  mounted () {
    this.get();
  },
  methods: {
    get(){
      this.$http.get('http://students.test/api/courses')
      .then(response => (this.courses = response.data.data))
    },
    edit(id){
      this.$http.get('http://students.test/api/courses/' + id)
      .then(response => (this.course = response.data.data))
    },
    resetCourse(){
        this.course = {
          id:null,
          teacher_name: null,
          name: null,
        };
    },
    create(){
      this.errors = null;

      if(this.course.id !== null){
        this.$http.patch('http://students.test/api/courses/' + this.course.id, this.course)
          .then(response => {
            this.get();
            this.resetCourse();
            alert(response.data.message);
          })
          .catch(e => {
            this.errors = e.response.data.errors;
            alert(e.response.data.message);
          })
      }else{
        this.$http.post('http://students.test/api/courses', this.course)
          .then(response => {
            this.get();
            this.resetCourse();
            alert(response.data.message);
          })
          .catch(e => {
            this.errors = e.response.data.errors;
            alert(e.response.data.message);
          })
      }

      
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
