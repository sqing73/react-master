## JSX
`JSX` is syntax sugar for `createElement`, which returns a **React** element.

**React** component's `$$typeof` records type of element and type records if it s a class of function component.

`JSX` only contains information for the component, and it does not contain information about `schedule`, `reconcile`, and `render`.
- During mount phase, `Reconciler` generate `Fiber` node based on `JSX` arguments
- During update, `Reconciler` compares `JSX` and `Fiber` node to and generate and also tags the new `Fiber` node.

## Workflow
`workLoopConcurrent` and `workLoopConcurrentByScheduler` is the entrypoint to create new nodes. It itratively iterate over the tree and updates it whenever there is time remaining in the current flow (`!shouldYield()`).

They further call `performUnitOfWork`. Notice the line

```
const current = unitOfWork.alternate;
```

`alternate` is bidirectional, i.e., the `current` node's alternate points to `workInProgress` and vice versa.

Initially, only `rootFiber` has `current` so we can use
```
current === null
```
to check if the node is in mounting or updating phase.

`performUnitOfWork` calls the `beginWork`. Based on the type of node (e.g. `FunctionComponent`), it generates new node and `reconcileChildren`, which adds the `effectTag` (like `update`, `place`) to the node if it is a updating phase.

Then how to mount the tree, since only update phase will place the `place` tag. The answer is only the `rootFiber` will be `placed` so there is only one DOM updates, instead of doing this for each node.

The `Fiber` node is kind of different from common tree node, which stores an array including all children. Instead `Fiber` node contains parent/`return` node and `sibling` node, like a linked list of linked list. This is due to array manipulation's overhead for supporting interruptible concurrency, and to avoid pre-consuming some memories.

Tomorrow let's start on completeWork, where the `stateNode` will be inserted.
