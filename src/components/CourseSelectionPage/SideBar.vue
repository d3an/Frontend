<template>
<v-card id="selection-sidebar"> 
    <v-list-item v-if="!majorRequirements.length && !minorRequirements.length && !specRequirements.length" id="no-program-message">
        Select a program above to get a list of requirements
    </v-list-item>
    <div class="sidebar-req-container" :class="checkMobile() ? 'side-req-container-mobile' : '' " >
        <RequirementDropdown v-bind:programArray="majorRequirements" />
        <RequirementDropdown v-bind:programArray="minorRequirements" />
        <RequirementDropdown v-bind:programArray="specRequirements" />
    </div>
    <p></p>
</v-card> 
</template>

<script>
import { mapGetters } from "vuex";
import RequirementDropdown from './RequirementDropdown';
import isMobile from 'ismobilejs';


export default {
    name: "SideBar",
    components: {
        RequirementDropdown
    },
    data() {
        return {
            lastClickdownReq: null
        }
    },
    methods: {
        checkMobile() {
         return isMobile(window.navigator).any
       },
    },
    computed: mapGetters(["majorRequirements", "minorRequirements", "specRequirements"]),
}
</script>

<style scoped>
#selection-sidebar {
    display: flex;
    flex-direction: column;
    width: 100%;
    background-color: #A0BDD6;
    overflow-x: hidden;
    overflow-y: hidden;
}

.sidebar-req-container {
    overflow-y: scroll;
    overflow-x: hidden;
    padding-left: 15px;
    margin-top: 7.5%;
    scrollbar-width: thin;
    scrollbar-color: #FFD646 #A0BDD6;
}

/* Somehow the scroll bar is not shown in native browsers so we need to add the padding */
.side-req-container-mobile {
    padding-right: 15px;
}

.sidebar-req-container::-webkit-scrollbar-thumb {
    background-color: #FFD646;
    border-radius: 20px;
    border: 4px solid #A0BDD6;

}

.sidebar-req-container::-webkit-scrollbar-track {
    background: #A0BDD6;
}

.required-course {
    margin: 0.75rem
}

.requirement-title {
    margin: 0.75rem;    
    padding: 0.5rem;
}

.course-card {
    margin: 1rem;
    text-align: left;
}

#no-program-message {
    color: #071223 !important;
}

.v-expansion-panel-content__wrap {
    padding-top: 0px !important;
    padding-right: 0px !important;
    padding-bottom: 0px !important;
    padding-left: 0px !important;
}

.title {
    text-align: left;
    padding-left: 24px;
    padding-top: 0.75rem;
    padding-bottom: 0.75rem;
    font-weight: 400;
    background-color: white;
}
</style>
