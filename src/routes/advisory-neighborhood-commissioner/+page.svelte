<script>
	import { setContext } from "svelte";
	import { browser } from "$app/environment";
	import Meta from "$components/Meta.svelte";
	import Index from "$components/ANC/Index.svelte";

	// Import the functions you need from the SDKs you need
	import { initializeApp } from "firebase/app";
	import { getAnalytics } from "firebase/analytics";
	// TODO: Add SDKs for Firebase products that you want to use
	// https://firebase.google.com/docs/web/setup#available-libraries

	// Your web app's Firebase configuration
	// For Firebase JS SDK v7.20.0 and later, measurementId is optional
	if (typeof window !== "undefined") {
		const firebaseConfig = {
			apiKey: "AIzaSyC1tArtXay0JCpWXemszeDZA8jFrO5aZUw",
			authDomain: "electeddc-2024-quiz.firebaseapp.com",
			projectId: "electeddc-2024-quiz",
			storageBucket: "electeddc-2024-quiz.appspot.com",
			messagingSenderId: "772337424714",
			appId: "1:772337424714:web:c4b132a1dcef70a9b889b3",
			measurementId: "G-F66CRNW7TM"
		};

		// Initialize Firebase
		const app = initializeApp(firebaseConfig);
		const analytics = getAnalytics(app);
	}
</script>

<Meta />
<Index />
