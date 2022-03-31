<template>
  <div main="trackcertpage">
        <div class="bg-white flex flex-col font-sans">
            <div class="w-screen shadow-lg"> 
                <div class="container mx-auto px-8">
                    <header class="flex flex-col sm:flex-row items-center justify-between relative">
                        <img class="scale-75 " src="../assets/images/tinago.png">
                        <nav class="hidden md:flex text-md">
                        <a @click="gthome" class="text-gray-800 hover:text-teal-400 py-3 px-6">Home</a>
                        <a @click="gttrackcert" class="text-gray-800 hover:text-teal-400 py-3 px-6">Appointment</a>
                        <a @click="gtreqcert" class="text-gray-800 hover:text-teal-400 py-3 px-6">Schedule an Appointment</a>
                        <a @click="$store.dispatch('logout')" class="bg-amber-500 hover:bg-teal-300 rounded-full uppercase text-white py-3 px-6">Log out</a>
                        </nav>
                    </header>
                </div>
            </div>
            <div class="bg-gray-200 mt-3 h-screen">
                <div v-if="clearanceExist" class="flex justify-evenly mt-1 py-10 ">
                    <div v-if="currentClearance" class="relative w-1/3 px-10 py-10 rounded-lg border-2 bg-gray-100 border-gray-500">
                        <div class="absolute right-3 top-3 ">
                            <text @click="editc" class="text-4xl material-icons text-amber-500 cursor-pointer mr-2 hover:text-amber-300">edit</text>                        
                            <text @click="Cdelete" class="text-4xl material-icons text-amber-500 cursor-pointer hover:text-amber-300">cancel</text>
                            
                        </div>
                        <div class="flex relative">
                            <h1 class="text-xl font-semibold text-left">Barangay Clearance</h1>
                        </div>
                        <hr class="mb-1 border-t border-teal-400 w-3/4" />
                        <div class="flex">
                            <p class="font-semibold text-justify text- mt-4 text-cyan-600">Name: </p>
                            <text class=" ml-3 font-semibold text-justify text-md mt-4 text-gray-800">{{cname}}</text>
                        </div>
                        <div class="flex">
                            <p class="font-semibold text-justify text-md mt-4 text-cyan-600">Appointment Date: </p>
                            <text class=" ml-3 font-semibold text-justify text-md mt-4 text-gray-800">{{cdate}}</text>
                        </div>
                        <div class="flex">
                            <p class="font-semibold text-justify text-md mt-4 text-cyan-600">Satus: </p>
                            <text class=" ml-3 font-semibold text-justify text-md mt-4 text-gray-800">{{cstatus}}</text>
                        </div>
                    </div>  
                    <div v-if="editClearance" class="relative w-2/3 px-10 py-10 rounded-lg border-2 bg-gray-100 border-gray-500">
                    <h1 class="text-xl font-semibold text-left">Barangay Clearance</h1> 
                        <div class="absolute right-3 top-3 ">                       
                            <text @click="canceleditc" class="text-4xl material-icons text-amber-500 cursor-pointer hover:text-amber-300">cancel</text>
                        </div>
                                <div class="flex mt-5 text-left">
        
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">First Name</label>
                                        <input v-model="newcfirst" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="First Name"/>
                                    </div>
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Midle Name</label>
                                        <input v-model="newcmiddle" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="Middle Name"/>
                                    </div>
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Last Name</label>
                                        <input v-model="newclast" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="Last Name"/>
                                    </div>
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Suffix</label>
                                        <input v-model="newcsuffix" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="Suffix"/>
                                    </div>
                                </div>
                                <div class="flex mt-5 text-left">
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Purok</label> 
                                        <select v-model="newcpurok" 
                                        class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent">
                                            <option value= "purok1">Purok 1</option>
                                            <option value= "purok2">Purok 2</option>
                                            <option value= "purok3">Purok 3</option>
                                        </select>
                                    </div>
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Citizenship</label>
                                        <input v-model="newccitizenship" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="Citizenship" />
                                    </div>
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Status</label>
                                        <select v-model="newcstatus" 
                                        class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent">
                                            <option value= "Single">Single</option>
                                            <option value= "Married">Married</option>
                                            <option value= "Widowed">Widowed</option>
                                            <option value= "Divorced">Divorced</option>
                                            <option value= "Separated">Separated</option>
                                        </select>
                                    </div>
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Age</label>
                                        <input v-model="newcage" class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent" type="text" placeholder="Age" />
                                    </div>
                                </div>
                                <div class="flex mt-5 text-left">
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="uppercase md:text-sm text-xs text-gray-500 text-light font-semibold">Quantity</label>
                                        <select v-model="newcquantity" 
                                        class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent">
                                            <option value= "1">1</option>
                                            <option value= "2">2</option>
                                        </select>
                                    </div>
                                    <div class="grid grid-cols-1 px-3 w-1/4">
                                        <label class="block mt-2 text-xs font-semibold text-gray-600 uppercase ml-2">Include Cedula</label>
                                        <select v-model="newccedula" 
                                        class="py-2 px-3 rounded-lg border-2 border-teal-400 mt-1 focus:outline-none focus:ring-2 focus:ring-purple-600 focus:border-transparent">
                                            <option value= "Yes">Yes</option>
                                            <option value= "No">No</option>                                            
                                        </select>
                                    </div>
                                    <div class="absolute right-10 mt-10 flex">
                                        <div @click="SaveClearanceInfo" class="w-32 h-10 rounded-full bg-amber-500 hover:bg-amber-300 mt-3 text-center cursor-pointer text-xl text-white font-medium py-1 mr-2">Save</div> 
                                    </div>
                                </div>
                    </div>  
                    <div v-if="deleteclearance" class="relative w-1/3 px-10 py-10 rounded-lg border-2 bg-gray-100 border-gray-500">
                        
                        <div class="flex relative">
                            <h1 class="text-xl font-semibold text-left">Barangay Clearance</h1>
                        </div>
                        <hr class="mb-1 border-t border-teal-400 w-3/4" />
                        <div class="justify-evenly right-10 mt-10 flex">
                            <div @click="confirmdelete" class="w-32 h-10 rounded-full bg-amber-500 hover:bg-amber-300 mt-3 text-center cursor-pointer text-xl text-white font-medium py-1 mr-2">Delete</div> 
                            <div @click="canceldelete" class="w-32 h-10 rounded-full bg-amber-500 hover:bg-amber-300 mt-3 text-center cursor-pointer text-xl text-white font-medium py-1 mr-2">Cancel</div> 
                        </div>
                    </div>
                </div> 
                <div v-if="empty" class="flex justify-evenly mt-1 py-10 h-screen object-center">
                    <div class=" w-1/2 px-10 py-10 object-center">
                        <text class=" text-4xl text-amber-500 cursor-pointer mr-2 hover:text-amber-300">You have no pending transactions at the moment</text>
                    </div>    
                </div> 
            </div>
        </div>
  </div>
</template>

<script>

import { app, auth  } from "../firebase";
import { clearanceColRef } from "../firebase";
import { getFirestore, getDoc, doc, setDoc,deleteDoc} from "firebase/firestore";

export default {
    data(){        
        return {
        ReqType:'',

        cname:'', cstatus:'', ctime:'', cdate:'',
        newcfirst:'', newcmiddle:'', newclast:'', newcsuffix:'', newcpurok:'', newccitizenship:'',newcstatus:'',newcage:'',newcquantity:'',newccedula:'',

        clearanceExist:false, currentClearance:false, editClearance:true, deleteclearance:false,
        empty:true,
        };
    },
     mounted(){
       this.loadrequests();
     },
    methods:{
        async loadrequests(){ 
           const db = getFirestore(app)
           const userid = auth.currentUser.uid;  
           const clearanceRef = doc(db, "Clearance Requests",userid);
           const clearanceSnap = await getDoc(clearanceRef);  
           if(clearanceSnap.exists()){
                console.log("Document data:", clearanceSnap.data());
                this.clearanceExist=true;
                this.currentClearance=true;
                this.editClearance=false;
                this.empty=false;
                this.cname = clearanceSnap.data().BCfirst + " " +clearanceSnap.data().BClast;
                this.cstatus = "Pending";
                this.cdate = clearanceSnap.data().BCdate;

                this.newcfirst = clearanceSnap.data().BCfirst;
                this.newcmiddle = clearanceSnap.data().BCmiddle;
                this.newclast = clearanceSnap.data().BClast;
                this.newcsuffix = clearanceSnap.data().BCsuffix;
                this.newcpurok = clearanceSnap.data().BCpurok;
                this.newccitizenship = clearanceSnap.data().BCcitizenship;
                this.newcstatus = clearanceSnap.data().BCstatus;
                this.newcage = clearanceSnap.data().BCage
                this.newcquantity = clearanceSnap.data().BCquantity;
                this.newccedula = clearanceSnap.data().BCcedula;


           } else{
                console.log("No such document!"); 
                this.empty=true;
           }
       },
       Cdelete(){
           this.ReqType = "CLEARANCE";
           this.deleteclearance = true;
           this.currentClearance = false;
       },
        editc(){
            this.clearanceExist=true;
            this.currentClearance=false;
            this.editClearance=true;
        },
        async SaveClearanceInfo(){
            
            var cost = 0;
            if(this.icedula == 'Yes'){
                cost = cost + 60;
            }
                
            const BCtotalcost = cost + 70*this.newcquantity;
            const BCdate = this.cdate;
            const BCtime = this.ctime;   
            const BCfirst = this.newcfirst;
            const BCmiddle = this.newcmiddle;
            const BClast = this.newclast;
            const BCsuffix = this.newcsuffix;
            const BCpurok = this.newcpurok;
            const BCcitizenship = this.newccitizenship;
            const BCstatus = this.newcstatus;
            const BCage = this.newcage;
            const BCquantity = this.newcquantity;
            const BCcedula = this.newccedula;

            const db = getFirestore(app);
            const currendID = auth.currentUser.uid;
            console.log("Creating Data");
            const addedDocs = await setDoc(doc(db, "Clearance Requests",currendID ),{currendID, BCdate, BCtime, BCfirst, BCmiddle, BClast, BCsuffix, BCpurok, BCcitizenship, BCstatus, BCage, BCquantity, BCcedula, BCtotalcost});
            alert("Changes Saved");
            console.log(addedDocs)
            this.loadrequests();
            
        },
        canceleditc(){
            this.clearanceExist=true;
            this.currentClearance=true;
            this.editClearance=false;
        },

        canceldelete(){
            this.deleteclearance = false;
            this.loadrequests();
        },
        async confirmdelete(){
            if(this.ReqType == "CLEARANCE"){
            let cleRef = doc(clearanceColRef,auth.currentUser.uid);
            await deleteDoc(cleRef);
            alert("deleted");
            this.ReqType = '';
            this.deleteclearance = false;
            console.log("deleted");
            this.loadrequests();
            }

        },

        gthome(){
        this.$router.push("/homepage");
        },
        gttrackcert(){
        this.$router.push("/trackcertpage");
        },
        gtreqcert(){
        this.$router.push("/requestcertpage");
        },
    }
}
</script>
