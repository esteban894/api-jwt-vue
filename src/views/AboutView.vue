<template>
	<div class="about">
		<h1>Ruta protegida</h1>
		{{ token }}
	</div>
</template>

<script>
import { mapState } from "vuex";

export default {
	computed: {
		...mapState(["token"]),
	},
	methods: {
		async datosProtegidos() {
			try {
				const res = await fetch("http://localhost:3001/api/admin", {
					headers: {
						"Content-Type": "application/json",
						"auth-token": this.token,
					},
				});
				const dataDB = await res.json();
				console.log(dataDB);
			} catch (error) {
				console.log(error);
			}
		},
	},
	created() {
		this.datosProtegidos();
	},
};
</script>

<style>
@media (min-width: 1024px) {
	.about {
		min-height: 100vh;
		display: flex;
		align-items: center;
	}
}
</style>
