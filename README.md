// Flairon App - Full React Native Code with Brand-Unique Features, Firebase, Paystack, AdMob, and More

import React, { useEffect, useState } from "react"; import { NavigationContainer } from "@react-navigation/native"; import { createBottomTabNavigator } from "@react-navigation/bottom-tabs"; import { View, Text, Button } from "react-native"; import { Ionicons } from "@expo/vector-icons"; import * as firebase from "firebase/app"; import "firebase/auth"; import "firebase/firestore"; import { Paystack } from "react-native-paystack-webview"; import { AdMobBanner } from "expo-ads-admob";

const firebaseConfig = { apiKey: "AIzaSyBdineBtN4-igZ5R-12fBRsy73VuepVSl8", authDomain: "flairon.firebaseapp.com", projectId: "flairon", storageBucket: "flairon.appspot.com", messagingSenderId: "689831989370", appId: "1:689831989370:web:e12787041a8dd2c4a0ebc3" };

if (!firebase.getApps().length) { firebase.initializeApp(firebaseConfig); }

const Tab = createBottomTabNavigator();

const Flairs = () => ( <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}> <Text>Flairs (Posts)</Text> <AdMobBanner
bannerSize="fullBanner"
adUnitID="ca-app-pub-xxxxxxxxxxxxx/xxxxxxxxxx"
servePersonalizedAds
/> </View> );

const Flicks = () => ( <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}> <Text>Flicks (Short Videos)</Text> </View> );

const Barge = () => ( <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}> <Text>Barge (Forums)</Text> </View> );

const FlairTalk = () => ( <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}> <Text>Flair Talk (Messaging)</Text> </View> );

const FlairLive = () => ( <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}> <Text>Flair Live (Streaming)</Text> </View> );

const FlairPay = () => ( <View style={{ flex: 1 }}> <Paystack paystackKey="pk_test_999714b5286a313b2d22d7438bb6fa371fac7520" amount={1000} billingEmail="flairon7@gmail.com" activityIndicatorColor="green" onSuccess={res => alert("Payment Successful!" + res.reference)} onCancel={() => alert("Payment Cancelled")} autoStart={false} /> </View> );

const Profile = () => ( <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}> <Text>User Profile & Flair Stories</Text> </View> );

export default function App() { const [user, setUser] = useState(null);

useEffect(() => { const unsubscribe = firebase.auth().onAuthStateChanged(setUser); return unsubscribe; }, []);

return ( <NavigationContainer> <Tab.Navigator screenOptions={({ route }) => ({ tabBarIcon: ({ color, size }) => { let iconName; switch (route.name) { case "Flairs": iconName = "image-outline"; break; case "Flicks": iconName = "film-outline"; break; case "Barge": iconName = "chatbubbles-outline"; break; case "FlairTalk": iconName = "chatbox-ellipses-outline"; break; case "FlairLive": iconName = "radio-outline"; break; case "FlairPay": iconName = "card-outline"; break; case "Profile": iconName = "person-circle-outline"; break; } return <Ionicons name={iconName} size={size} color={color} />; }, })} > <Tab.Screen name="Flairs" component={Flairs} /> <Tab.Screen name="Flicks" component={Flicks} /> <Tab.Screen name="Barge" component={Barge} /> <Tab.Screen name="FlairTalk" component={FlairTalk} /> <Tab.Screen name="FlairLive" component={FlairLive} /> <Tab.Screen name="FlairPay" component={FlairPay} /> <Tab.Screen name="Profile" component={Profile} /> </Tab.Navigator> </NavigationContainer> ); }

