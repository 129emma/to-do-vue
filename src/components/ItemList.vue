<template>
        <el-card class="box-card">
            <el-container>
                <el-header>
                    <!-- <item-input>
                    </item-input> -->
                    <el-input  
                        placeholder="What needs to be done?"
                        v-model="itemInput"
                        @keyup.enter.native="addNewItem"
                        >
                    </el-input> 
                </el-header>
                <el-main>
                    <span v-show = "!itemList.length" class="noTask"> No task yet</span>
                    
                        
                            <div>
                                <ul @click="openTdList(toDoList)">
                                    <li class="active">
                                        <a href="#">TO DO 
                                            <span>{{itemList.length}}</span>
                                        </a>
                                    </li>
                                </ul>
                                <ul v-show="toDoList">
                                    <!-- :key is optional -->
                                    <!-- set index as key to prevent duplicate key detection -->
                                    <li 
                                    v-for="(item, index) in itemList"
                                    :key="index" 
                                    @click.stop="finishItem(index)"
                                    >    
                                        <p v-bind:title="item.name">
                                            {{ item.name }}
                                            <span class="deletIcon" @click.stop="removeTdItem(item)" >
                                                <i class="el-icon-close">
                                                </i>
                                            </span>
                                        </p>
                                    </li>
                                </ul>
                            </div>
                        

                        
                            <div>
                                <ul @click="openHdList(hvDoneList)">
                                    <li class="active">
                                        <a href="#">Completed 
                                            <span class="badge">{{doneList.length}}</span>
                                        </a>
                                    </li>
                                </ul>
                                <ul v-show="hvDoneList">
                                    <li
                                    v-for="(item, index) in doneList"
                                    :key="index" 
                                    >
                                        <p v-bind:title="item.name" :class="{finish: item.isFinished}">
                                            {{ item.name }}
                                            <span class="deletIcon" @click.stop="removeHdItem(item)" >
                                                <i class="el-icon-close">
                                                </i>
                                            </span>
                                        </p>
                                    </li>
                                </ul>
                            </div>
                        
                       
                </el-main>
                <el-footer> 
                    <el-row>
                        <el-col :span="8">
                            <div>
                                <p v-if="itemList.length > 1" >{{ itemList.length }} items left</p>
                                <p v-else>{{ itemList.length }} item left</p>
                            </div>
                        </el-col>
                        <el-col :span="8">
                            <div>
                              <!-- <el-button @click="openHdList(hvDoneList)">
                                    TO DO
                              </el-button>   -->
                            </div>
                        </el-col>
                        <el-col :span="8">
                            <el-button type="danger" plain>
                                        Clear All
                            </el-button>
                        </el-col>
                    </el-row>
                </el-footer>
            </el-container> 
        </el-card>   
</template>

<script>
// import ItemInput from './ItemInput.vue';

    export default {
        data() {
            return {
                itemInput: '',
                itemList: [
                ],
                doneList: [
                ],
                checked: false,
                editItem: '',
                beforeEdit: '',
                toDoList: true,
                hvDoneList: false,
                selectItems: '',
                isFinished: false

            }
        },
        methods: {
            addNewItem() {
                let text = this.itemInput.trim()
                if (!text) {
                    return;
                } else {
                    this.itemList.push({
                    name: text
                    })
                    this.itemInput = ''
                } 
            },
            finishItem(index) {
                this.doneList.push({
                    name: this.itemList[index].name,
                    isFinished: true
                })
                this.itemList.splice(index,1)
            },
            removeTdItem(item) {
                this.itemList.splice(item, 1)
            },
            removeHdItem(item) {
                this.doneList.splice(item, 1)
            },
            openTdList(item) {
                this.toDoList = !item
            },
            openHdList(item) {
                this.hvDoneList = !item
            }
        },
        directives:{
        "focus":{
            update(el,binding){
                if(binding.value){
                    el.focus();
                }
            }
        }
    },
}
</script>

<style scoped>
li {
    list-style-type: none;
    padding-top: 20px
}
.finish {
    text-decoration: line-through
}
.noTask {
    color: lightslategray
}
.itemArea {
    display: none;
}
.deletIcon {
    margin-left: 100px
}

</style>
