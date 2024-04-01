import firebase from "firebase";

var firebaseConfig = {
    apiKey: "AIzaSyBXdx41wjOD9OZGwz9AvL2ZDRXMImvkGWU",
    authDomain: "auth-9764f.firebaseapp.com",
    projectId: "auth-9764f",
    storageBucket: "auth-9764f.appspot.com",
    messagingSenderId: "460079948542",
    appId: "1:460079948542:web:73e79db4a70ed91dd8fbaf"
  };
  // Initialize Firebase
  firebase.initializeApp(firebaseConfig);
  const db = firebase.firestore();
  const auth = firebase.auth();

  export {auth};
  export default db;



//////////////////////////// google sign in ///////////////////////

import firebase from 'firebase';
import {useState,useEffect} from 'react';

firebase.initializeApp({
  apiKey: "",
    authDomain: "",
    projectId: "",
    storageBucket: "",
    messagingSenderId: "",
    appId: ""
})
const auth = firebase.auth();

const App = () => {
  const [user,setUser] = useState(null);
useEffect(()=>{
  auth.onAuthStateChanged(person=> {
    if(person){
      setUser(person)
    }
    else{
      setUser(null)
    }
  })
})
const signInWithGoogle = async () =>{
  try{
    await auth.signInWithPopup(new firebase.auth.GoogleAuthProvider());
  }
  catch(err){
    console.log(err);
  }
}

  return (
    <div>
        <center>
          {user?
          <div>
           <h1>Welcome to home page </h1>
          <button onClick={()=>auth.signOut()}>Sign Out</button>
          </div>
          :
          <button onClick={signInWithGoogle}>Sign In With Google</button>}
          
        </center>
    </div>
  )
}

export default App
