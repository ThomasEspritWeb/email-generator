<template>
  <div class="container-fluid">
    <h3 class="mb-4">Le générateur de mails</h3>
    <div class="row">
      <div class="col-md-7">
        <div class="card">
          <div class="card-header text-white"><b>1 - A remplir</b></div>
          <div class="card-body">
            <small class="text-muted">Renseigner ci-dessous les coordonnées du recruteur à qui vous souhaitez envoyer un mail</small>
            <form class="mt-4">
              <div class="row mb-4">
                <div class="col-lg-2">
                  <label for="civilite" class="col-form-label">Civilité</label>
                </div>
                <div class="col-lg-10">
                  <select name="civilite" class="form-control" v-model="civilite">
                    <option value="">SELECTIONNER</option>
                    <option value="Monsieur">Monsieur</option>
                    <option value="Madame">Madame</option>
                  </select>
                </div>
              </div>
              <div class="row mb-4">
                <div class="col-lg-2">
                  <label for="prenom" class="col-form-label">Prénom</label>
                </div>
                <div class="col-lg-4">
                  <input type="text" name="prenom" class="form-control" placeholder="Ex: Paul" v-model="prenom">
                </div>
                <div class="col-lg-2">
                  <label for="nom" class="col-form-label">Nom</label>
                </div>
                <div class="col-lg-4">
                  <input type="text" name="nom" class="form-control" placeholder="Ex: Dupont" v-model="nom">
                </div>
              </div>
              <div class="row mb-4">
                <div class="col-lg-2">
                  <label for="entreprise" class="col-form-label">Entreprise</label>
                </div>
                <div class="col-lg-10">
                  <input type="text" name="entreprise" class="form-control" placeholder="Ex: Apple" v-model="entreprise">
                </div>
              </div>
              <div class="row mb-4">
                <div class="col-lg-2">
                  <label for="poste" class="col-form-label">Poste</label>
                </div>
                <div class="col-lg-10">
                  <input type="text" name="poste" class="form-control" placeholder="Ex: Chargé de recrutement" v-model="poste">
                </div>
              </div>
              <div class="row mb-4">
                <div class="col-12 mb-4">
                  <small class="text-muted">Renseigner ci-dessous l'objet et le contenu du mail en utilisant les variables. Elles seront remplacées automatiquement dans la partie "<b>2 - Email à envoyer</b>"</small>
                  <div class="p-2 mb-2 mt-2 bg-info text-white">
                    Vous pouvez utiliser les variables suivantes :
                    <span class="badge bg-light text-dark mr-1">&#123;&#123;civilite&#125;&#125;</span>
                    <span class="badge bg-light text-dark mr-1">&#123;&#123;prenom&#125;&#125;</span>
                    <span class="badge bg-light text-dark mr-1">&#123;&#123;nom&#125;&#125;</span>
                    <span class="badge bg-light text-dark mr-1">&#123;&#123;entreprise&#125;&#125;</span>
                    <span class="badge bg-light text-dark mr-1">&#123;&#123;poste&#125;&#125;</span>.
                    <br>
                    Ex : Bonjour <span class="badge bg-light text-dark mr-1">&#123;&#123;civilite&#125;&#125;</span><span class="badge bg-light text-dark mr-1">&#123;&#123;nom&#125;&#125;</span> > Bonjour Monsieur Dupont
                  </div>
                </div>
                <div class="col-lg-2">
                  <label for="objet" class="col-form-label">Objet</label>
                </div>
                <div class="col-lg-10">
                  <input type="text" name="objet" class="form-control" v-model="objet" placeholder="Ouvrez ce mail &#123;&#123;prenom&#125;&#125;">
                </div>
              </div>
              <div class="mb-3">
                <label for="contenu" class="col-form-label">Corps du mail</label>
                <textarea name="contenu" class="form-control" rows="20" v-model="contenu" placeholder="Renseigner ici le corps du mail avec les variables disponibles. Ex : Bonjour {{civilite}} {{nom}}"></textarea>
              </div>
            </form>
          </div>
        </div>
      </div>
      <div class="col-md">
        <div class="card">
          <div class="card-header text-white"><b>2 - Email à envoyer</b></div>
          <div class="card-body">
            <div class="mb-2">
              <label class="col-form-label">Objet</label>
              <input type="text" disabled class="form-control" :value="objetText">
            </div>
            <div class="mb-2">
              <label class="col-form-label">Corps du mail</label>
              <textarea rows="20" disabled class="form-control" id="contenuText" v-model="contenuText"></textarea>
            </div>
          </div>
        </div>

      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'MailGenerator',
  data(){
    return{
      prenom:'',
      nom:'',
      entreprise:'',
      objet:'',
      contenu:'',
      civilite:'',
      poste: ''
    }
  },
  computed:{
    objetText(){
      return this.replaceVariables(this.objet)
    },
    contenuText(){
      return this.replaceVariables(this.contenu)
    }
  },
  methods:{
    replaceVariables(text){
      return text.replace('{{prenom}}', this.prenom)
                  .replace('{{nom}}', this.nom)
                  .replace('{{entreprise}}', this.entreprise)
                  .replace('{{civilite}}', this.civilite)
                  .replace('{{poste}}', this.poste)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-info{
  border-radius: 0.25rem;
}

.card{
  border: none;
}

.card-header{
  background-color: #6F7D95;
}

.col-form-label{
  text-transform: uppercase;
  font-size: 0.75rem;
  font-weight: bold;
  color: #6F7D95;
}
</style>
