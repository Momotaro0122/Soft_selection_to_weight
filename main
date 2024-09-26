import maya.OpenMaya as om
import maya.cmds as cmds

def soft_selection_getter():
    selection = om.MSelectionList()
    softSelection = om.MRichSelection()
    om.MGlobal.getRichSelection(softSelection)
    softSelection.getSelection(selection)
    
    dagPath = om.MDagPath()
    component = om.MObject()
    weights = []
    
    iter = om.MItSelectionList(selection, om.MFn.kMeshVertComponent)
    while not iter.isDone():
        iter.getDagPath(dagPath, component)
        dagPath.pop()
        node = dagPath.fullPathName()
        fnComp = om.MFnSingleIndexedComponent(component)
        for i in range(fnComp.elementCount()):
            index = fnComp.element(i)
            weight = fnComp.weight(i).influence()
            weights.append((node, index, weight))
        iter.next()
    
    for node, index, weight in weights:
        print(node, index, weight)
    return weights
soft_selection_getter()
