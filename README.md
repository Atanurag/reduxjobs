# reduxjobs


/*
function local() {
	
let li=localStorage.getItem("explist");
let arr=[];

if(li){

arr=JSON.parse(li);

}
return arr;


}
*/


function mylocal1() {
let lo=localStorage.getItem("explist");
let a=[];

if(lo){
a=JSON.parse(lo);

}

return a;
}

function mylocal2() {
	let loc=localStorage.getItem("contact");
let b=[];

if(loc){
b=JSON.parse(loc);

}
return b;
}




const initialstate={

list:mylocal1(),
	linkdin:[],
	contacts:mylocal2(),
	check:false,
	vari:"",
	cou:0,
	login:[{na:"hello",id:0}],
	user:null

};

const changeTheNumber=(state=initialstate,action)=>{

switch(action.type){

case "addtocart":

//let appe=[...state.list,{...action.payload}]
///state.list.push(action.payload)
let productsindex=state.list.findIndex((inddd)=>inddd.id===action.payload.id);

if(productsindex>=0){
state.list[productsindex].quantity+=1;

}


else{


let temp={...action.payload,quantity:1}

localStorage.setItem("explist",JSON.stringify([...state.list,temp]));
//localStorage.setItem("explist",JSON.stringify([...state.list,temp]));

return {
...state,
list:[...state.list,temp],


}
}




break;
case "remtocart":

const deleted=state.list.filter((arr)=>  arr==action.payload)

localStorage.setItem('explist',JSON.stringify(deleted));
//localStorage.setItem("explist",JSON.stringify(deleted));

return {
	...state
,
list:deleted,


}
break;
case "increment":

let indexqu=state.list.findIndex((qua)=> qua.id===action.payload.id )
state.list[indexqu].quantity+=1;
localStorage.setItem('explist',JSON.stringify([...state.list]));
return {
...state,
list:[...state.list]

}

break;

//my practise actions
case "changevariab":
{/*if(action.payload.includes("a")){

	var sp=`${action.payload}: hogaya`;
}
else{
var sp=`${action.payload}: nhi`;

}*/
}
localStorage.setItem('contact',JSON.stringify([...state.contacts,action.payload]))


return {

...state,

contacts:[...state.contacts,action.payload]

//vari:sp

}



//my practise actions
break;

case "deleconts":

const delet=state.contacts.filter((de)=>{


	return de.id!==action.payload.id
})
localStorage.setItem('contact',JSON.stringify(delet))


return {

...state,

contacts:delet

//vari:sp

}






break;


case "decrement":

let indexq=state.list.findIndex((qua)=> qua.id===action.payload.id )

if(state.list[indexq].quantity>1){


	state.list[indexq].quantity-=1;
}

else if(state.list[indexq].quantity==1){

const deleted=state.list.filter((arr)=>  arr!=action.payload)
localStorage.setItem('explist',JSON.stringify(deleted));
return {
...state
,
list:deleted


}


}

else{

state.list[indexq].quantity=0;

}
return {
...state,
list:[...state.list]

}

break;
case "logidata":


return{
...state,
login:[...state.login,action.payload]
}

break;

case "edited":
console.log(action.payload,action.payload.updatedtext)

let update=state.login.map((up)=>{
if(up.id===action.payload.id){

return {...up,na:action.payload.updatedtext};
}

return up;
})


console.log(update)
return{
...state,
login:[...state.login,update]

}


default :
return state;
}

}
export default changeTheNumber;

/*

const initialstate=66;


const changeTheNumber=(state=initialstate,action)=>{

switch(action.type)
{
case "increment":
return state+action.pa;

case "decrement":
return state-1;

default :return state;
}
}

export default changeTheNumber;*/
