table_mapping = {'InsuredPersons':template_insured_person,
             'CoverageDetails':coverage_details}

Function to process the node which is of type *TABLE*

    Function fill_master_xml_table(master_element_node, master_node_tag, policy_xml, wrapper_nodes):
    
      list xml_node = [<master_node_tag>]
      list table_node = []

      #TODO: Get table names from table_mapping
      table_details = table_mapping.get(master_node_tag)


      #TODO: To get master_xml_node_children
      master_xml_node_children = master_node_original.child
      wrapper_xml_node = wrapper_nodes.pop(master_node_tag)  
      #TODO: take count of the number of table_elements (rows present in the wrapper_xml)
      num_subelement = length(wrapper_xml_node.child)

      #TODO: Get children of table elements in master xml
      master_xml_node_child_children = master_xml_node_children.child

      for i in num_subelement:
          table_node.add(<master_xml_node_child.tag>)

          for master_xml_node_child_child in master_xml_node_child_children:
              table_column_tag = master_xml_node_child_child.tag
              #CASE: if column present in wrapper xml
              #TODO: get column from wrapper xml and add it to the table node
              if master_xml_node_child_child.tag is present in wrapper_xml_node_child[i].child:
                  column_node = wrapper_xml_node_child[i].pop(table_column_tag)
                  column_node_text = node_to_string(column_node)
                  table_node.add(<table_column_tag>column_node_text</ table_column_tag>)

              #CASE: if column name in not present in the wrapper xml
              #TODO: add column name from master_xml
              else:
                  table_node.add(<table_column_tag / >)

          table_node.add(</ master_xml_node_child>)  


      return xml_node

            
        
       
        
        


    Function CreateXml(wrapper_xml, master_xml):

      list updated_xml = []
      #policy_xml = main_xml['Policy']                     #the get the element 'Policy' 
      wrapper_nodes = wrapper_xml.child
      master_nodes = master_xml.child



      #TODO: Iterate over the nodes of master xml (childrens of 'policy')
      for master_element_node in master_nodes:
          master_node_tag = master_element_node.tag

          #CASE 1: When node of master xml is present in wrapper xml; when node type is table
          #TODO: Add the node of type table form wrapper xml
          if master_node_tag is present in wrapper_nodes:
              # node is a table
              xml_node = fill_master_xml_table(master_element_node, master_node_tag, policy_xml, wrapper_nodes)
              updated_xml.add(xml_node)

          #CASE 2: When a node of master xml is not present in wrapper xml
          else:
              xml_node.add(<mastser_node_tag>)
              #TODO: get all childern if master xml node
              master_xml_node_children =  master_element_node.child


              #TODO: iterate over all the childern of master_xml_node
              for master_xml_node_child in master_xml_node_children:
                  #CASE 2.1: When table is present in the master xml but not in wrapper_nodes
                  #TODO: 1.Check whether master_xml_node_child have any children
                  #        If TRUE: then the node is of type table; otherwiese it is field-vlaue pair
                  if master_xml_node_child.child Exist:
                      xml_node.add(<master_xml_node_child.tag>) 
                      #TODO: Iterate over the children of master_xml_node_child
                      #      to search for the case where table value of master_xml_node_child 
                      #      is present as field value in wrapper_nodes


                      for master_xml_node_child_child in master_xml_node_child.child:
                          #CASE 2.1.1: When element of master xml table is present as field-value pair in wrapper_nodes
                          #TODO: Get the node from wrapper xml and add it to xml_node (updated xml)
                          if master_xml_node_child_child is present in wrapper_nodes:
                              wrapper_xml_node = wrapper_nodes.pop(master_xml_node_child_child.tag)
                              wrapper_node_text = node_to_text(wrapper_xml_node)
                              xml_node.add(wrapper_node_text)

                          #CASE 2.1.2: When master_node_child_child [element of table] is not present in wrapper_nodes as field-value pair
                          #TODO: Get the master_node_child_child node and add it to the xml_node (updated xml)
                          else:
                              master_xml_node_child_child_text = node_to_text(master_xml_node_child_child)
                              xml_node.add(master_xml_node_child_child_text)


                        xml_node.add(</master_xml_node_child.tag>) 


                  #CASE 2.2: When fileld-value pair of master_xml [master_xml_node_child] is present in wrapper_nodes
                  #TODO: Get the field-value node form wrapper_xml_node_child and add to the xml_node (updated_xml)
                  else, if master_xml_node_child.tag is present in wrapper_nodes:
                       #case when single value is present in wrapper xml
                       wrapper_xml_node = wrapper_nodes.pop(master_xml_node_child.tag)
                       wrapper_xml_node_text = node_to_text(wrapper_xml_node)
                       xml_node.add(wrapper_xml_node_text)

                  #CASE 2.3: When field-value pair of master_xml_node is not present in the wrapper_nodes
                  #TODO: Get the field-value node from master_xml_node_child and add it to node_xml (updated_xml)
                  else, if master_xml_node_child is not present in wrapper.child:
                      master_xml_node_child_text = node_to_string(master_xml_node_child)
                      xml_node.add(master_xml_node_child_text)


              xml_node.add(</ master_node_tag>)    






              #if node is not present in wrapper xml then copy that node as it is
              policy_xml_node_string = node_to_string(policy_xml[i])
              updated_xml.add(policy_xml_node_string)

        return string_to_text(updated_xml)
 
