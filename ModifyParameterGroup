public void ModifyParameterGroup()
		{
			Document doc = this.ActiveUIDocument.Document;
			Autodesk.Revit.ApplicationServices.Application application = doc.Application;
			
			Dictionary<string, ForgeTypeId> paramDict = new Dictionary<string, ForgeTypeId>();

			//other
			paramDict.Add("R_TEST", GroupTypeId.Phasing);
			paramDict.Add("R_UniqueCatID", GroupTypeId.Phasing);

			BindingMap bindingsMap = doc.ParameterBindings;
			DefinitionBindingMapIterator iterator = bindingsMap.ForwardIterator();

			using (Transaction t = new Transaction(doc, "Change Parameter Group"))
			{
				t.Start();
				while (iterator.MoveNext())
				{
					ElementBinding elementBinding = iterator.Current as ElementBinding;
					Definition definition = iterator.Key;

					InternalDefinition intDef = definition as InternalDefinition;

					if (paramDict.ContainsKey(definition.Name))
						intDef.SetGroupTypeId(paramDict[definition.Name]);
				}
				t.Commit();
			}
		}
