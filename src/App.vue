<template>
  <v-app>
    <v-navigation-drawer v-model="isDrawerOpen">
      <v-list>
        <v-list-subheader>Menu</v-list-subheader>
        <v-list-item prepend-icon="mdi-home">Home</v-list-item>
        <v-list-item prepend-icon="mdi-account">Usuários</v-list-item>

        <v-list-group value="Clientes">
          <template #activator="{ props }">
            <v-list-item
              v-bind="props"
              prepend-icon="mdi-account-circle"
              title="Clientes"
            ></v-list-item>
          </template>

          <v-list-item prepend-icon="mdi-currency-usd">Vendas</v-list-item>
          <v-list-item prepend-icon="mdi-chart-line">Relatório</v-list-item>
        </v-list-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar flat class="border-b">
      <v-app-bar-nav-icon
        @click="isDrawerOpen = !isDrawerOpen"
      ></v-app-bar-nav-icon>
      <v-app-bar-title> Site de Viagens </v-app-bar-title>

      <template #append>
        <v-btn icon class="mr-2">
          <v-badge dot color="info">
            <v-icon icon="mdi-bell-outline"> </v-icon>
          </v-badge>
        </v-btn>
        <v-menu>
          <template #activator="{ props }">
            <v-avatar v-bind="props">
              <v-img
                cover
                src="data:image/png;base64,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"
                >\
              </v-img>
            </v-avatar>
          </template>
          <v-card min-width="200px">
            <v-list :lines="false" density="compact" nav>
              <v-list-item prepend-icon="mdi-account-outline">
                <v-list-item-title>Meu perfil</v-list-item-title>
              </v-list-item>

              <v-list-item prepend-icon="mdi-heart-outline">
                <v-list-item-title>Favoritos</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-card>
        </v-menu>
      </template>
    </v-app-bar>
    <v-main>
      <v-container>
        <h1 class="mb-6" v-ripple>Localizações</h1>

        <v-card falt class="border mb-4">
          <div class="d-flex justify-space-between" >
             <v-card-title>Últimos usuários </v-card-title>

             <v-card-title >   
              <v-btn @click="isDialogOpen = true" variant="tonal" size="small">Adicionar usuário</v-btn>
              <v-dialog
              v-model="isDialogOpen" 
              width="600px">
                
                <v-card>
                  <v-card-title>Adicionar usuário</v-card-title>
                  <v-card-text>
                    <v-row>
                      <v-col>
                        <v-text-field label="Nome" variant="outlined" ></v-text-field>
                      </v-col>
                      <v-col>
                        <v-text-field label="Email" variant="outlined" :rules="emailRules"></v-text-field>
                      </v-col>
                    </v-row>

                    <v-select label="Cargo" 
                    variant="outlined"
                    :items="['Adimin', 'Gerente', 'Convidado']">
                  </v-select>
                  </v-card-text>

                  <v-card-actions>
                    <v-space></v-space>
                    <v-btn variant="tonal" color="text">
                      Cancelar
                    </v-btn>
                    <v-btn variant="tonal" color="success">
                      Salvar
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
             </v-card-title>
             
           
          </div>
         

          <v-table density="compact">
            <thead>
              <tr>
                <th>Nome</th>
                <th>Email</th>
                <th>Cargo</th>
                <th>Ações</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Jose</td>
                <td>Jose@gmail.com</td>
                <td>
                  <v-chip color="primary" variant="outlined" size="small">Admin</v-chip>
                </td>
                <td>
                  <v-btn
                    icon="mdi-pencil"
                    variant="tonal"
                    color="primary"
                  ></v-btn>
                </td>
              </tr>
              <tr>
                <td>Lucas</td>
                <td>Lucas@gmail.com</td>
                <td>
                  <v-chip color="success" variant="outlined" size="small">Gerente</v-chip>
                </td>
                <td>
                  <v-btn
                    icon="mdi-pencil"
                    variant="tonal"
                    color="primary"
                  ></v-btn>
                </td>
              </tr>
              <tr>
                <td>Marcos</td>
                <td>Marcos@gmail.com</td>
                <td>
                  <v-chip variant="outlined" size="small">Convidado</v-chip>
                </td>
                <td>
                  <v-btn
                    icon="mdi-pencil"
                    variant="tonal"
                    color="primary"
                  ></v-btn>
                </td>
              </tr>
            </tbody>
          </v-table>
        </v-card>

        <v-row>
          <v-col cols="12" sm="6" md="4" lg="3">
            <v-card flat class="border">
              <v-img
                class="align-start text-white"
                src="https://images.pexels.com/photos/13966075/pexels-photo-13966075.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
              >
                <v-card-title> Top 10 praias na Bahia </v-card-title>
              </v-img>
              <v-card-subtitle class="pt-3"> Salvador </v-card-subtitle>
              <v-card-text>
                <div>Rio vermelho</div>
                <div>Praias incríveis</div>
              </v-card-text>
              <v-card-action>
                <v-btn variant="tonal" color="info">Ver mais</v-btn>
                <v-btn variant="tonal" color="info">Comprar</v-btn>
                <v-btn icon="mdi-home" variant="tonal" color="info"></v-btn>
              </v-card-action>
            </v-card>
          </v-col>

          <v-col cols="12" sm="6" md="4" lg="3">
            <v-card flat class="border">
              <v-img
                class="align-start text-white"
                src="https://images.pexels.com/photos/13966075/pexels-photo-13966075.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
              >
                <v-card-title> Melhores pontos turísticos do Rio </v-card-title>
              </v-img>
              <v-card-subtitle class="pt-3"> Rio de janeiro </v-card-subtitle>
              <v-card-text>
                <div>Cristo Redentor</div>
                <div>Pão de açucar</div>
              </v-card-text>
              <v-card-action>
                <v-btn variant="tonal" color="info">Ver mais</v-btn>
                <v-btn variant="tonal" color="info">Comprar</v-btn>
                <v-btn icon="mdi-home" variant="tonal" color="info"></v-btn>
              </v-card-action>
            </v-card>
          </v-col>

          <v-col cols="12" sm="6" md="4" lg="3">
            <v-card flat class="border">
              <v-img
                class="align-start text-white"
                src="https://images.pexels.com/photos/12791979/pexels-photo-12791979.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
              >
                <v-card-title> Melhores lugares do Sul </v-card-title>
              </v-img>
              <v-card-subtitle class="pt-3"> Gramado </v-card-subtitle>
              <v-card-text>
                <div>Lugares aconchegantes</div>
                <div>Venha conferir</div>
              </v-card-text>
              <v-card-action>
                <v-btn variant="tonal" color="info">Ver mais</v-btn>
                <v-btn variant="tonal" color="info">Comprar</v-btn>
                <v-btn icon="mdi-home" variant="tonal" color="info"></v-btn>
              </v-card-action>
            </v-card>
          </v-col>

          <v-col cols="12" sm="6" md="4" lg="3">
            <v-card flat class="border">
              <v-img
                class="align-start text-white"
                src="https://images.pexels.com/photos/12791979/pexels-photo-12791979.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
              >
                <v-card-title> Melhores lugares do Sul </v-card-title>
              </v-img>
              <v-card-subtitle class="pt-3"> Gramado </v-card-subtitle>
              <v-card-text>
                <div>Lugares aconchegantes</div>
                <div>Venha conferir</div>
              </v-card-text>
              <v-card-action>
                <v-btn variant="tonal" color="info">Ver mais</v-btn>
                <v-btn variant="tonal" color="info">Comprar</v-btn>
                <v-btn icon="mdi-home" variant="tonal" color="info"></v-btn>
              </v-card-action>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template> 

<script setup>
import { ref } from "vue";

const isDrawerOpen = ref(false);
const isDialogOpen = ref(false);
const emailRules=[
  value => {
    if(value) return true;

    return 'O email é obrigatório';
  }
];
</script>
