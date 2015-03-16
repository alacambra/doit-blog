Recently I have confronted the problem to updates fields of a dataTable using the jsf ajax tag. Here my solution:

```xml
<h:column>
	<f:facet name="header">
		<h:outputText value="#{bundle.ListIngredientTitle_name}" />
	</f:facet>
	<h:panelGroup id="pg">
		<div id="edit_#{ingredient.id}" style="display: none;">
			<h:inputText id="sid" styleClass="edit-label" value="#{ingredient.name}" size="10" />
          <f:ajax execute="sid" render="messagePanel pg">
              <h:commandButton value="ok" action="#{ingredientController.commitEdition}" />
          </f:ajax>
          <span onclick="cancelEdit('#{ingredient.id}')">cancel</span>
		</div>
		<div id="read_#{ingredient.id}">
			<span class="read-label" onclick="setEditMode('#{ingredient.id}')">#{ingredient.name}</span>
		</div>
	</h:panelGroup>
</h:column>
```

Each updatable columnhas two components:

* Edit mode.
* Read mode. 

The edit panel has commandButton to submit the update. It is wrapped by the ajax tag since that will be the element that performs the ajax call. 
As **execution** id I am giving the id of the inputText (the value to be sent and updated) and as a **render** fields, the complete panel that wraps both components to assure that the values will be correctly updated. I am also passing an extra id in the render field which is being used by another element to show feedback messges like "successfully updated", or "some error".
The js functions are only responsible for the toggling of both modes, and they have no further interest.
After this expirience, I would say that to use the ajax on jsf, three points must be clear:

* Which **element is going to perform the update**. This element will contents the ajax tag or can be wrapped by it.

*  Which **values** are going **to be sent**. Their ids will be given to the **execution** attribute.

*  After the ajax response, which **element** needs **to be rerendered or repaint**. Their ids will be given to the **render** attribute.

In the code, you can see that I am using ids in a static way like ```<h:panelGroup id="pg"> ``` or in a dynamic way like ```<div id="edit_#{ingredient.id}" style="display: none;">```. That is because jsf components are generated before to render the EL expression and therefore the ID would be empty. However, jsf is intelligent enough to know that each element ID needs to be unique and will generate a unique ID (remember that this code belongs to a concrete row). All jsf component will be able to reference this ID (in our case the ```<ajax>``` tag). In the other hand plain html elements will not receive automatically a unique ID but we can give it dynamiccally. I am using this ID in the js code. These conclusion are achieved just by observation, so if it is not true or partially wrong, I would be glad to know how exactly is it working.

The complete code can be found [here](https://github.com/alacambra/ruthchenchens-cooking-helper/blob/50379c508edf8db9aed9b7d2edbfef5eb0499249/src/main/webapp/ingredient/List.xhtml).