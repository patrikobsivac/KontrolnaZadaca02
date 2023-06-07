
<template>
	<v-container fill-height fluid class="background">
		<v-row>
			<v-col cols="12">
				<v-card class="pa-3" outlined width="600px">
					<v-card-title>Unos Studenata</v-card-title>
					<v-card-text>
						<v-form ref="form" v-model="valid">
							<v-row>
								<v-col>
									<v-text-field
										label="Ime"
										required
										v-model="ime"
										:rules="imeRules"
									></v-text-field>
								</v-col>
							</v-row>
							<v-row>
								<v-col>
									<v-text-field
										label="Prezime"
										required
										v-model="prezime"
                                        :rules="prezimeRules"
									></v-text-field>
								</v-col>
							</v-row>
							<v-row>
								<v-col>
									<v-text-field
										label="Indeks"
										required
										prefix="RS"
										v-model="indeks"
                                        :rules="indeksRules"
									></v-text-field>
								</v-col>
							</v-row>
							<v-row>
								<v-col>
									<v-text-field
										label="Godina Upisa"
										required
										v-model="godinaUpisa"
                                        :rules="godinaUpisaRules"
									></v-text-field>
								</v-col>
							</v-row>
							<v-row>
								<v-col>
									<v-text-field
										label="Broj Bodova Prvog Kolokvija"
										required
										v-model="x1"
                                        :rules="x1Rules"
									></v-text-field>
								</v-col>
							</v-row>
							<v-row>
								<v-col>
									<v-text-field
										label="Broj Bodova Drugog Kolokvija"
										required
										v-model="x2"
                                        :rules="x2Rules"
									></v-text-field>
								</v-col>
							</v-row>
							<v-row>
								<v-col>
									<v-text-field
										label="Broj Dolazaka"
										required
										v-model="dolazak"
                                        :rules="dolazakRules"
									></v-text-field>
								</v-col>
							</v-row>
							<v-row>
								<v-col>
									<v-text-field
										label="Kontinuirano Pracenje"
										required
										v-model="kontinuiranoPracenje"
                                        :rules="kontinuiranoPracenjeRules"
									></v-text-field>
								</v-col>
							</v-row>
						</v-form>
					</v-card-text>
					<v-card-actions>
						<v-btn
							:disabled="!valid"
							color="black"
							class="white--text"
							elevation="0"
							@click="dodajStudenta"
						>
							DODAJ STUDENTA
						</v-btn>
						<v-btn
							color="black"
							class="white--text"
							elevation="0"
							@click="ocistiFormu"
						>
							OCISTI FORMU
						</v-btn>
						<v-btn
							color="black"
							class="white--text"
							elevation="0"
							@click="obrisiSveUnesenePodatke"
						>
							BRISI PODATKE
						</v-btn>
						<v-spacer></v-spacer>
					</v-card-actions>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "prvi-zadatak",
	data() {
		return {
            ime: "",
            prezime: "",
            indeks: "",
            godinaUpisa: "",
            x1: "",
            x2: "",
            dolazak: "",
            kontinuiranoPracenje: "",
            valid: true,
            imeRules: [(value) => value.length !== 0 || "Ime je obavezno"],
            prezimeRules: [(value) => value.length !== 0 || "Prezime je obavezno"],
            indeksRules: [(value) => value.length !== 0 || "Indeks je obavezno"],
            godinaUpisaRules: [(value) => value.length !== 0 || "Godina upisa je obavezno"],
            x1Rules: [(value) => value > 50 || "Kolokvij mora prelaziti preko 50%"],
            x2Rules: [(value) => value > 50 || "Kolokvij mora prelaziti preko 50%"],
            dolazakRules: [(value) => value > 11 || "Broj dolazaka mora biti veći od 11"],
            kontinuiranoPracenjeRules: [(value) => value > 5 || "Kontinuirano praćenje mora biti veće od 5"]
        };
	},
	watch: {},
	methods: {
		ocistiFormu() {
            this.$refs.form.reset();
		},
		dodajStudenta() {
			let noviStudent = {
				ime: this.ime, 
				prezime: this.prezime,
                indeks: this.indeks,
                godinaUpisa: this.godinaUpisa,
                x1: this.x1,
                x2: this.x2,
                dolazak: this.dolazak,
                kontinuiranoPracenje: this.kontinuiranoPracenje
			};
			//ovo ne diraj
			let studenti = JSON.parse(localStorage.getItem("studenti"));
			if (!studenti) {
				studenti = [];
			}
			studenti.push(noviStudent);
			localStorage.setItem("studenti", JSON.stringify(studenti));
		},
		obrisiSveUnesenePodatke() {
			localStorage.clear();
		},
	},
};
</script>