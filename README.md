# Integrating-Expense-tracker-

<div class="container">
    <div class="form-group">
      <label for="itemAmount">Enter Amount:</label>
      <input type="number" class="form-control" id="itemAmount">
      <label for="itemDescription">Enter Description:</label>
      <input type="text" class="form-control" id="itemDescription">
  
      <label for="itemSelect">Select Item:</label>
      <select class="form-control" id="itemSelect">
        <option>Movie</option>
        <option>Cafe</option>
        <option>Bar</option>
      </select>
  
      <button type="button" class="btn btn-primary" onclick="addItem()">Add Item</button>
      <ul class="list-group mt-3" id="itemList"></ul>
    </div>
  </div>
  
  <!-- JavaScript code -->
  <script>
    var itemList = document.getElementById('itemList');
    var items = [];
  
    function addItem() {
      // Get selected item from dropdown
      var itemSelect = document.getElementById('itemSelect');
      var selectedItem = itemSelect.options[itemSelect.selectedIndex].text;
  
      // Get entered amount and description
      var itemAmount = document.getElementById('itemAmount').value;
      var itemDescription = document.getElementById('itemDescription').value;
  
      // Create item object and add to items array
      var item = {
        amount: itemAmount,
        description: itemDescription,
        category: selectedItem
      };
      items.push(item);
  
      // Clear input fields
      itemSelect.selectedIndex = 0;
      document.getElementById('itemAmount').value = "";
      document.getElementById('itemDescription').value = "";
  
      // Update item list
      updateItemList();
    }
  
    function updateItemList() {
      // Clear item list
      itemList.innerHTML = "";
  
      // Loop through items array and create list item for each
      for (var i = 0; i < items.length; i++) {
        var item = items[i];
  
        // Create list item
        var listItem = document.createElement('li');
        listItem.innerHTML = item.amount + " - " + item.description + " - " + item.category;
  
        // Create delete button
        var deleteBtn = document.createElement('button');
        deleteBtn.innerHTML = "Delete";
        deleteBtn.classList.add('btn', 'btn-danger', 'mx-2');
        deleteBtn.onclick = function() {
          // Get index of item in items array
          var index = Array.prototype.indexOf.call(itemList.children, this.parentNode);
  
          // Remove item from items array and update item list
          items.splice(index, 1);
          updateItemList();
        };
        listItem.appendChild(deleteBtn);
  
        // Create edit button
        var editBtn = document.createElement('button');
        editBtn.innerHTML = "Edit";
        editBtn.classList.add('btn', 'btn-secondary');
        editBtn.onclick = function() {
          // Get index of item in items array
          var index = Array.prototype.indexOf.call(itemList.children, this.parentNode);
  
          // Get item from items array
          var item = items[index];
  
          // Set input fields to item values
          document.getElementById('itemAmount').value = item.amount;
          document.getElementById('itemDescription').value = item.description;
          document.getElementById('itemSelect').value = item.category;
  
          // Remove item from items array and update item list
          items.splice(index, 1);
          updateItemList();
        };
        listItem.appendChild(editBtn);
  
        // Add list item to item list
        itemList.appendChild(listItem);
      }
    }
  </script>
  