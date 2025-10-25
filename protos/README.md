# Strategic Action Tracker - Proto Models

This directory contains Protocol Buffer (protobuf) definitions for the Strategic Action Tracker application's data models.

## Proto Files

### AuditEntry.proto
Common audit tracking information used across multiple entities.
- **date_created**: Timestamp when the entry was created
- **created_by**: Username of the user who created the entry
- **date_modified**: Timestamp when the entry was last modified
- **modified_by**: Username of the user who last modified the entry

### StrategicGoal.proto
Main entity representing a strategic goal.
- **id**: Primary key (integer)
- **name**: Name of the strategic goal
- **goal_references**: Collection of GoalReference objects
- **audit_entry**: Audit tracking information

### GoalReference.proto
External references or resources associated with a strategic goal.
- **id**: Primary key (integer)
- **goal_key**: Foreign key to StrategicGoal
- **name**: Name of the resource
- **url**: Link URL to the resource
- **display_text**: Display text for the reference type
- **audit_entry**: Audit tracking information

### GoalEvent.proto
Events or milestones related to a strategic goal.
- **id**: Primary key (integer)
- **goal_key**: Foreign key to StrategicGoal
- **event_date**: Date when the event occurred
- **description**: Description of the event
- **audit_entry**: Audit tracking information

### GoalAction.proto
Action items that need to be completed for a strategic goal.
- **id**: Primary key (integer)
- **goal_key**: Foreign key to StrategicGoal
- **action_description**: Description of the required action
- **action_assigned_to**: Username of the person assigned to the action
- **action_status**: Status of the action (e.g., "Not Started", "In Progress", "Waiting for Reply", "Completed")
- **audit_entry**: Audit tracking information

### GoalNote.proto
Notes or comments associated with a strategic goal.
- **id**: Primary key (integer)
- **goal_key**: Foreign key to StrategicGoal
- **note_text**: Text content of the note
- **audit_entry**: Audit tracking information

### ActionTag.proto
Join table linking actions to tags.
- **action_tag_id**: Primary key (integer)
- **action_id**: Foreign key to GoalAction
- **tag_id**: Foreign key to Tag

### Tag.proto
Tags that can be applied to actions for categorization.
- **id**: Primary key (integer)
- **tag_name**: Display text of the tag
- **audit_entry**: Audit tracking information

## Compilation

To compile these proto files, use the protobuf compiler (`protoc`):

```bash
# Example: Generate Python code
protoc --proto_path=. --python_out=./generated protos/*.proto

# Example: Generate C# code
protoc --proto_path=. --csharp_out=./generated protos/*.proto

# Example: Generate Java code
protoc --proto_path=. --java_out=./generated protos/*.proto
```

## Notes

- All proto files use `proto3` syntax
- Date/time fields use `google.protobuf.Timestamp` for consistency
- Foreign key relationships are represented using `int32` fields with `_key` suffix
- The `repeated` keyword is used for one-to-many relationships (e.g., `goal_references`)
- All files are in the `strategic_action_tracker` package namespace
