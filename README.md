<!Document html>
<html>
    <head>
        <meta charset="utf-8">
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">
        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
        <title>List contact</title>
    </head>
    <body class="text-center">
             <nav class="navbar navbar-light bg-light">
                <div class="form-inline mx-auto">
                    <input type="text" class="search form-control mr-sm-2" onchange="clearInput()" placeholder="Поиск" aria-    label="Поиск">
                    <button onclick="search()" class="btn btn-outline-success">
                    Поиск</button>
                </div>
            </nav>
<!--        <nav class="navbar navbar-light bg-light">-->
            <div class="container">
                <div class="row">
                    <div class="col">
                        <label class="badge badge-default mt-2 mb-2">Имя и Фамилия:</label>
                        <br>
                        <input type="text" class="name mt-1">
                    </div>
                    <div id="divTel" class="colm">
                        <label class="badge badge-default mt-2 mr-4">Номер телефон:</label>
                        <br>
                        <input  type="number" class="number"> 
                        <button onclick="addTel()" class="btn btn-link">+</button>
                        <br>
                    </div>  
                
                    <div id="divAdress" class="col">
                        <label class="badge badge-default mt-2 mr-5">Адрес:</label>
                        <br>
                        <input type='text' class="adress">
                        <button onclick="addAdress()" class="btn btn-link">+</button>
                        <br>
                    </div>          
                    <div id="divEmail" class="col">
                        <label class="badge badge-default mt-2 mr-5">Email:</label>
                        <br>
                        <input type="email" class="email">
                        <button onclick="addEmail()" class="btn btn-link">+</button>
                        <br>
                    </div>   
                </div>
                       
                <div class="row">
                    <div class="col mt-3 mb-3">
                        <button onclick="addContact()" class="addcontact btn btn-outline-success">Добавить</button>       
                        <button onclick="updateContact()" class="editContact btn btn-outline-info">Заменить</button>
                        <button onclick="clearForm()" class="clearForm btn btn-outline-warning">Очистить форму</button>
                    </div>    
              </div>
    </div> 
<!--            </nav>-->
        
        <table class="table table-dark">
        <thead>
          <tr>
            <td scope="col">Имя и Фамилия</td>
            <td scope="col" >Номер телефон</td>
            <td scope="col">Адрес</td>
            <td scope="col">Email</td>
            </tr>
          </thead>
          <tbody id="tbody">
           
          </tbody>
          
        </table>
        <script>
            document.getElementsByClassName('editContact')[0].style.visibility = 'hidden';
            var numPhone=0;
            function addTel() {
                var element = document.getElementById('divTel');
                numPhone = numPhone + 1;
                createTag(element, 'Номер тел ', numPhone, 'number');           
            }
            var numAdress = 0;
            function addAdress() {
                var element = document.getElementById('divAdress');
                numAdress = numAdress + 1;
                createTag(element, 'Адрес', numAdress, 'adress');           
            } 
            var numEmail = 0;
            function addEmail() {
                var element = document.getElementById('divEmail');
                numEmail = numEmail + 1;
                createTag(element, 'Email', numEmail, 'email');           
            }
            
            
            function createTag(element, type, num, name) {
                var text = document.createElement('input');
                var br = document.createElement('br');
                var label = document.createElement('label');
                label.innerHTML = type + ' ' + num + ': ';
                text.setAttribute('class', name);
                element.appendChild(label);
                element.appendChild(text);
                element.appendChild(br);
            }
            
            // add contact to table
            var numForIdTagTr = 1;
            function addContact() {
                var tbody = document.getElementById('tbody');
                var tagTr = document.createElement('tr');
                var tdName = document.createElement('td');
                var tdNumber = document.createElement('td');
                var tdAdress = document.createElement('td');
                var tdEmail = document.createElement('td');
                var tdEdit = document.createElement('td');
                var tdDelete = document.createElement('td');
                var p = document.createElement('a');
                
                //var numeric = Number(document.getElementById('numberFoTagTr').value);
                //numForIdTagTr =+ 1;
                tagTr.setAttribute('id', 'tr' + numForIdTagTr);
                tagTr.setAttribute('class', 'tr');
                
                //add name and surname                
                tdName.innerHTML = document.getElementsByClassName('name')[0].value;                
                tagTr.appendChild(tdName);               
                               
                //add phone
                   let tagSpan           
                for(let i=0; i<document.getElementsByClassName('number').length; i++){
                    let br = document.createElement('br');
                    let tagInput = document.getElementsByClassName('number')[i];
                    tagSpan = document.createElement('span');
                    tagSpan.setAttribute('class', 'spanNumber');
                    tagSpan.innerHTML = tagInput.value;
                    tdNumber.appendChild(tagSpan);
                    tdNumber.appendChild(br);
                }
                
                tagTr.appendChild(tdNumber);
                
                //add adress
                
                for (let i=0; i<document.getElementsByClassName('adress').length; i++){
                    let tagInput = document.getElementsByClassName('adress')[i];
                    let br = document.createElement('br');
                    tagSpan = document.createElement('span');
                    tagSpan.setAttribute('class', 'spanAdress');
                    tagSpan.innerHTML = tagInput.value;
                    tdAdress.appendChild(tagSpan);
                    tdAdress.appendChild(br);
                }
                tagTr.appendChild(tdAdress);
                
                //add mail
                
                for (let i=0; i<document.getElementsByClassName('email').length; i++){
                    let tagInput = document.getElementsByClassName('email')[i];
                    let br = document.createElement('br');
                    tagSpan = document.createElement('span');
                    tagSpan.setAttribute('class', 'spanEmail');
                    tagSpan.innerHTML = tagInput.value;
                    tdEmail.appendChild(tagSpan);
                    tdEmail.appendChild(br);
                }
                tagTr.appendChild(tdEmail);
                
                // add button for update and delete               
                tdEdit.innerHTML = 'Изменить';
                tdEdit.setAttribute('onclick', 'editContact(tr' + numForIdTagTr + ')');
                tagTr.appendChild(tdEdit);
                tdDelete.innerHTML = 'Удалить';
                tdDelete.setAttribute('onclick', 'deleteContact(tr' + numForIdTagTr + ')');
                tagTr.appendChild(tdDelete);
                tbody.appendChild(tagTr);  
                
                clearForm();
                numForIdTagTr++;
            }
            
            //edit contactForm            
            var publicTag;
            function editContact (tagNum) {
                document.getElementsByClassName('editContact')[0].style.visibility = 'visible';
                document.getElementsByClassName('addContact')[0].style.visibility = 'hidden';
                
                var tr1 = tagNum.children;                
                document.getElementsByClassName('name')[0].value = tr1[0].innerHTML;
              //  console.log(tr1[1].children.length);
                let j=0;
               for (let i=0; i<tr1[1].children.length; i+=2){                   
                   document.getElementsByClassName('number')[j].value = tr1[1].children[i].innerHTML;
                   j++;
               }
                let g=0;
               for (let i=0; i<tr1[2].children.length; i+=2){                   
                   document.getElementsByClassName('adress')[g].value = tr1[2].children[i].innerHTML;
                   g++;
               } 
                let h=0;
               for (let i=0; i<tr1[2].children.length; i+=2){                   
                   document.getElementsByClassName('email')[h].value = tr1[3].children[i].innerHTML;
                   h++;
               }
                
                publicTag = tagNum;
            }    
            
            //update contact
            
            function updateContact(){
                var childTr = publicTag.children;
                childTr[0].innerHTML = document.getElementsByClassName('name')[0].value;
                 let numForNumber = 0;          
                for(let i=0; i<=document.getElementsByClassName('number').length; i+=2){
                    childTr[1].children[i].innerHTML = document.getElementsByClassName('number')[numForNumber].value;
                    numForNumber++;
                } 
                let numForAdress = 0;          
                for(let i=0; i<=document.getElementsByClassName('adress').length; i+=2){
                    childTr[2].children[i].innerHTML = document.getElementsByClassName('adress')[numForAdress].value;
                    numForAdress++;
                } 
                let numForEmail = 0;          
                for(let i=0; i<=document.getElementsByClassName('email').length; i+=2){
                    childTr[3].children[i].innerHTML = document.getElementsByClassName('email')[numForEmail].value;
                    numForEmail++;
                }
            }
            
            //delete contact
            
            function deleteContact(tagFoDelete){
                var tbody = document.getElementById('tbody');
                tbody.removeChild(tagFoDelete);
            }
            
            // search name
           
             function search(){
                 
                 var element = document.getElementsByClassName('search')[0].value;
                 var tagTd = document.getElementsByClassName('tr');
                 for (let i = 0; i < document.getElementsByClassName('tr').length; i++ ){
                     if (element == tagTd[i].children[0].innerHTML){                                
                         editContact(tagTd['tr' + (i+1)]);
                     }
                 }
                 document.getElementsByClassName('editContact')[0].style.visibility = 'hidden';
                document.getElementsByClassName('addContact')[0].style.visibility = 'visible';
             }
            
            //clear form
            function clearForm(){
                for (i=0; i<document.getElementsByTagName('input').length; i++){
                    document.getElementsByTagName('input')[i].value = '';
                }
            }
            
            function clearInput() {
                if(document.getElementsByClassName('search')[0].value == '') {
                    clearForm();
                }        
            }
        </script>
    </body>
</html>
